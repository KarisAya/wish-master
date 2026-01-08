# 不完美许愿器 (Wish Master)

**“So tell me, what is it you truly desire?”**

这是原地址[完美许愿器](https://github.com/senzi/wish-master)

[不完美许愿器](https://wish.karisaya.top/)

# 改动

`/api/validateWish`

**Method**: `POST`

**Description**: 一站式处理愿望审核与结果生成。

**请求体**:

```json
{
  "wish": "我想要点石成金的能力"
}
```

**响应体 (Success)**:

```json
{
  "status": "success",
  "result": {
    "category": "allow",
    "confirmed_wish": "我想要点石成金的能力",
    "scenario": "你的愿望实现了，但由于金价暴跌且你触碰的日常用品都变成了无用的重金属，你最终一贫如洗...",
    "score": 6 // 愿望逻辑得分 0-10
  },
  "debug_audit": { "..." } // 仅供调试参考
}

```
