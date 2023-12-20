# 中国人民大学半自动化抢课脚本

适用：时间优先选课阶段（即本学期末，下学期初）

支持：

- 整点运行
- 请求速度控制
- 自动重试
- 自动停止

## How to use

0. `pip install aiohttp ruclogin`

1. （**重要**）配置 [ruclogin](https://github.com/panjd123/ruclogin)

2. （可选）调整 `config.ini`

4. 获取要抢的课：`python collect.py` 等待选课界面加载后，选一遍要选的课，然后关掉浏览器

5. 执行脚本：`python main.py`

6. 抢到课或同类别选满会输出到控制台，速度监控会输出到文件 `ruccourse.log`，你可以观察日志文件来判断抢课是否在正常运行。

## Q&A

Q：运行原理？

A：暴力发选课请求，直到抢到，或者同类课达到选课上线。其实抢课的实现不复杂，但是之前的测试表明，cookies 容易失效，所以现在配合 [ruclogin](https://github.com/panjd123/ruclogin) 可以保证抢课不中断。

Q：有没有被检测的风险？

A：经过 2021-2023 年三年抢课的尝试，1000/s 的请求速度都没有出现过问题，当然，没必要设这么高，除非你们在科技对战？脚本默认参数是 30/s，已经足够。

Q：为什么是半自动化？

A：人大的教务系统写得“非常好”，抢课请求里面引入了一大堆意义不明，命名不明的不知道怎么填，不填还会炸的参数，研究清楚太费劲，遂采用抓包的方法。

## TODO

抓包和抢课阶段不一致的功能未经测试。

## 效果

抢别人后阶段退的课，实际上这种名额挺多的，我抢过：

- 社会主义500年
- 素质拓展
- 电影导论
- 后人类时代的全球影像

这些课最初的中签率都在 10% 到 30% 之间。