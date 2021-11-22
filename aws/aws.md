## AWS CLIでDYNAMOを見る

```
aws dynamodb scan --table-name serverless_blog_entries
```



```
[cloudshell-user@ip-10-0-160-103 ~]$ aws dynamodb scan --table-name serverless_blog_entries
{
    "Items": [
        {
            "text": {
                "S": "初投稿"
            },
            "created_at": {
                "S": "2021-11-22T23:15:37.325313+0000"
            },
            "id": {
                "N": "1637590537"
            },
            "title": {
                "S": "初"
            }
        }
    ],
    "Count": 1,
    "ScannedCount": 1,
    "ConsumedCapacity": null
}
```

