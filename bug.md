

# 1、 EOFError: Ran out of input
### 错误其实是pytorch函数torch.utils.data.DataLoader在windows下的特有错误，该函数里面有个参数num_workers表示进程个数，在windows下改为0就可以了，这个解答是在外国友人那边看到的，具体链接如下：https://discuss.pytorch.org/t/pytorch-windows-eoferror-ran-out-of-input-when-num-workers-0/25918/2

data.py
    # Create data loader
    #tr_set = DataLoader(tr_set, batch_size=tr_loader_bs, shuffle=shuffle, drop_last=drop_last, collate_fn=collect_tr,
    #                    num_workers=n_jobs, pin_memory=use_gpu)
    #dv_set = DataLoader(dv_set, batch_size=dv_loader_bs, shuffle=False, drop_last=False, collate_fn=collect_dv,
    #                    num_workers=n_jobs, pin_memory=pin_memory)
    tr_set = DataLoader(tr_set, batch_size=tr_loader_bs, shuffle=shuffle, drop_last=drop_last, collate_fn=collect_tr,
                        num_workers=0, pin_memory=use_gpu)
    dv_set = DataLoader(dv_set, batch_size=dv_loader_bs, shuffle=False, drop_last=False, collate_fn=collect_dv,
                        num_workers=0, pin_memory=pin_memory)

# 2、
  File "G:\src\NLP\2020HLP\End-to-end-ASR-Pytorch\src\audio.py", line 102, in forward
    waveform, sample_rate = torchaudio.load(filepath)
  File "D:\ProgramData\Anaconda3\envs\pytorch_gpu\lib\site-packages\torchaudio\backend\no_backend.py", line 20, in load
    raise RuntimeError('No audio I/O backend is available.')
RuntimeError: No audio I/O backend is available.
