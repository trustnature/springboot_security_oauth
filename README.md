SpringSecurity+OAuth2
原始的OAuth2.0 授权DEMO 可用来学习OAuth2.0 来用
使用数据库方式实现 未使用JWT令牌 

**第一步：用户授权**
http://localhost:9001/oauth/authorize?response_type=code&client_id=heima_two

**第二步：获取token**
http://localhost:9001/oauth/token
form-data
grant_type:authorization_code
client_id:heima_two
client_secret:123
code:上一步获取
响应：
{
    "access_token": "b062511c-eed6-4eaf-8372-74417253112e",
    "token_type": "bearer",
    "refresh_token": "45d91412-ab07-4254-a871-f81f5b368e80",
    "expires_in": 43199,
    "scope": "read ROLE_API ROLE_ADMIN write"
}

**第三步：check_token**
http://localhost:9001/oauth/check_token
x-www-form-rulencoded:
token:b062511c-eed6-4eaf-8372-74417253112e
响应报文：
{
    "aud": [
        "res1",
        "product_api"
    ],
    "user_name": "admin",
    "scope": [
        "read",
        "ROLE_API",
        "ROLE_ADMIN",
        "write"
    ],
    "active": true,
    "exp": 1635971001,
    "authorities": [
        "ROLE_PRODUCT",
        "ROLE_USER"
    ],
    "client_id": "heima_two"
}

**第四步：访问资源**
http://localhost:9002/product/findAll?access_token=b062511c-eed6-4eaf-8372-74417253112e

注意：此版本的authorities应该根据角色找到permission才对！
https://www.bilibili.com/video/BV1vt4y1i7zA