当然在测试时，我们肯定没有目标转换图片的，因为我们就是为了生成目标转换图片。为此，作者在训练好这个自编码网络后，将训练集中的目标转换图片利用该自编码网络抽取出最后一层的特征图，然后利用Instance-wise计算出要输入G网络的features map。接着利用k均值聚类对同一abel的所有样本的均值特征向量进行聚类得到K个聚类。这样我们在测试的时候，G网络根据label map的信息，对在每个label从之前聚类好的K个中心随机挑选一个特征，来生成G网络控制多样性的输入（features map）。

`    def get_edges(self, t):
        edge = torch.cuda.ByteTensor(t.size()).zero_()
        edge[:, :, :, 1:] = edge[:, :, :, 1:] | (t[:, :, :, 1:] != t[:, :, :, :-1])
        edge[:, :, :, :-1] = edge[:, :, :, :-1] | (t[:, :, :, 1:] != t[:, :, :, :-1])
        edge[:, :, 1:, :] = edge[:, :, 1:, :] | (t[:, :, 1:, :] != t[:, :, :-1, :])
        edge[:, :, :-1, :] = edge[:, :, :-1, :] | (t[:, :, 1:, :] != t[:, :, :-1, :])
        if self.opt.data_type == 16:
            return edge.half()
        else:
            return edge.float()`

`       edge_map = self.get_edges(inst_map)
        input_label = torch.cat((input_label, edge_map), dim=1)
        input_label = Variable(input_label, volatile=infer)`
