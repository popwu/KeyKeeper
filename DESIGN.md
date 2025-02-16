这是一个钱包，前后端分离
后端 mysql+ent+golang+gin
前端 react+tailwindcss

API 设计：
- 用户注册（私钥创建）
/api/create_private_key POST
{
    "password": "123456"
}
返回
{
    "session_token": "xxxx"
}

- 导出私钥
/api/export_private_key GET
header: session
{
    "password": "123456"
}
返回
{
    "private_key": "xxxx"
}

- 获取余额
/api/get_balance GET
header: session_token
返回
{
    // 本币余额
    "balances": 100
    // erc20 余额
    "erc20" : [
        {
            "name": "aaa",
            "balances": 100
        }
    ]
}

- 转账
/api/transfer POST
header: session_token
{
    "to": "0x123",
    "amount": 100,
    "coin": "eth"
}
返回
{
    "txid": "xxxx"
}

- 获取交易详情
/api/get_tx GET
header: session_token
{
    "txid": "xxxx"
}
返回
{
    "txid": "xxxx",
    "from": "0x123",
    "to": "0x123",
    "amount": 100,
    "coin": "eth",
    "status": "success"
}

- 获取交易列表
/api/get_tx_list GET
header: session_token
{
    "page": 1,
    "size": 10
}
返回
{
    "txs": [
        {
            "txid": "xxxx",
            "from": "0x123",
            "to": "0x123",
            "amount": 100,
            "coin": "eth",
            "status": "success"
        }
    ]
}