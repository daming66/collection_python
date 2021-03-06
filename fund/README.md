# 抓取基金重仓股

1. 本地安装 mysql 并创建数据库和数据表

```
def init_conn():
    global Connection, Table  # 全局使用
    url = "mysql+pymysql://root:wnnwnn@127.0.0.1:3306/testdb"  # 测试地址，改成你的本地 mysql 数据库地址
    engine = db.create_engine(url)
    metadata = db.MetaData()
    Connection = engine.connect()
    Table = db.Table(TableName, metadata, autoload=True, autoload_with=engine)
```

注意 url 里的地址改成你的本地的 mysql 地址。

```
url = "mysql+pymysql://user:password@127.0.0.1:3306/testdb"  # 测试地址，改成你的本地 mysql 数据库地址
```

```
CREATE TABLE `danjuan_fund_2020_4` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `fund_name` varchar(64) DEFAULT '' COMMENT '基金名称',
    `fund_code` varchar(16) NOT NULL DEFAULT '' COMMENT '基金代码',
    `managers` varchar(32) NOT NULL DEFAULT '' COMMENT '管理人',
    `enddate` varchar(32) NOT NULL DEFAULT '' COMMENT '季报日期',
    `detail_json` text NOT NULL COMMENT '蛋卷基金详细信息 json',
    PRIMARY KEY (`id`),
    KEY `idx_code` (`fund_code`),
    KEY `idx_name` (`fund_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

2. 安装 python3 依赖

```sh
pip3 install requests
pip3 install SQLAlchemy -i https://pypi.doubanio.com/simple --user
pip3 install pymysql -i https://pypi.doubanio.com/simple --user

# https://github.com/numpy/numpy/issues/15947 numpy 版本高有问题
pip3 install numpy==1.18.0 -i https://pypi.doubanio.com/simple
pip3 install pandas -i https://pypi.doubanio.com/simple
pip3 install openpyxl -i https://pypi.doubanio.com/simple
```

3. 运行代码 `python danjuan.py`
