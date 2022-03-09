### Add IP:
```
/v1/info/add_ip and it takes ip as params
```
#### data:
 - 'ip': ip_adderss [CharField]
#### response:
| status code | possible responses/errors |
| ----------- | ------------------------- |
| 201 | "success": True, "message": "IP has been updated" |
| 400 | "success": False, "messaeg": "bad request" |
| 401 | "success": False, "messaeg": "wrong jwt" |
| 404 | "success": False, "messaeg": "machine number does not exist" |
