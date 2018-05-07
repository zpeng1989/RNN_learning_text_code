一个基于最新版本TensorFlow的Char RNN实现。可以实现生成英文、写诗、歌词、小说、生成代码、生成日文等功能。


## 需求
- Python 3.6.X
- TensorFlow >= 1.2

## 生成英文文本

训练模型:

```
python train.py --input_file data/shakespeare.txt --name shakespeare --num_steps 50 --num_seqs 32 --learning_rate 0.01 --max_steps 20000
```

测试结果:

```
python sample.py --converter_path model/shakespeare/converter.pkl --checkpoint_path model/shakespeare/ --max_length 1000
```


## 生成诗歌

训练模型:

```
python train.py --use_embedding --input_file data/poetry.txt --name poetry --learning_rate 0.005 --num_steps 26 --num_seqs 32 --max_steps 10000
```

测试结果:

```
python sample.py --use_embedding --converter_path model/poetry/converter.pkl --checkpoint_path model/poetry/ --max_length 300
```


## 生成小说，时间长，CPU(i7)十万次迭代需要24个小时，需要适当修改max_steps参数，如果gpu速度快很多

novel.txt 为输入训练数据，需要修改为 utf-8 编码，这个需要在notepad里面自行整理

训练模型：

```
python train.py --use_embedding True --input_file data/novel.txt --num_steps 80 --name novel --learning_rate 0.005 --num_seqs 32 --num_layers 3 --embedding_size 256 --lstm_size 256 --max_steps 1000000
```

测试结果:

```
python sample.py --converter_path model/novel/converter.pkl --checkpoint_path  model/novel --use_embedding --max_length 20000 --num_layers 3 --lstm_size 256 --embedding_size 256
```

## 生成歌词，输入为周杰伦歌词

训练模型:

```
python train.py --input_file data/jay.txt --num_steps 20 --batch_size 32 --name jay --max_steps 5000 --learning_rate 0.01 --num_layers 3 --use_embedding
```

测试结果, 其中start_string参数后面为你要创建歌曲的歌名字:

```
python sample.py --converter_path model/jay/converter.pkl --checkpoint_path  model/jay --max_length 500 --use_embedding --num_layers 3 --start_string 我知道
```

## 生成 Linux 系统脚本

训练模型:

```
python train.py --input_file data/linux.txt --num_steps 100 --name linux --learning_rate 0.01 --num_seqs 32 --max_steps 20000
```

生成模型:

```
python sample.py --converter_path model/linux/converter.pkl --checkpoint_path  model/linux --max_length 1000 
```


## 生成日语文章

训练模型:
```
python train.py --input_file data/jpn.txt --num_steps 20 --batch_size 32 --name jpn --max_steps 10000 --learning_rate 0.01 --use_embedding
```

生成模型:
```
python sample.py --converter_path model/jpn/converter.pkl --checkpoint_path model/jpn --max_length 1000 --use_embedding
```


