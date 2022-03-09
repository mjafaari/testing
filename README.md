### Add IP
```
/v1/info/add_ip and it takes ip as params
```
#### data
'ip': $ip
| status code | possible responses/errors |
| ----------- | ------------------------- |
| 200 | "success": True, "message": "IP has been updated" |
| 201 | "success": False, "messaeg": "" |
