---
title: jwt
date: 2023-04-05 17:00:33
tags:
toc: true
published: false
---

#### 





### 什么是jwt

Jwt是JSON Web Tokens的简称，从单词可以看出它也是一种token，其实可以理解为一种生成token的框架或规范。既然也是token那我们可以换一种问法，token是什么？为什么要使用token？

### token是什么

Token是服务端生成的一串字符串，以作客户端进行请求的一个令牌，当第一次登录后，服务器生成一个Token便将此Token返回给客户端，以后客户端只需带上这个Token前来请求数据即可，无需再次带上用户名和密码

### 为什么使用token

Token是在客户端维护的一种机制，用于身份认证和授权。它是一个字符串，可以包含有关用户身份和权限的信息。在Web应用程序中，当用户成功登录后，服务器将颁发一个Token，然后将其发送给客户端。以后，客户端将在每个请求的HTTP头中包含该Token。服务器可以使用Token验证请求的来源和请求者的身份和权限。

### session和token有什么区别

1. Session和Token的存储位置不同。Session存储在服务器上，可以在服务器端直接修改和更新。Token存储在客户端上，通常使用localStorage或sessionStorage存储在浏览器中。
2. Session的存储容量通常比Token大，因为它可以存储更多的用户信息。Token通常只包含有关用户身份和授权的少量信息。
3. Session可以在一定时间内保持持久状态，而Token通常在一段时间后过期。
4. 在Web应用程序中，通常会同时使用Session和Token，以提供更加安全和可靠的身份认证和授权机制。Session通常用于维护用户状态和敏感信息，而Token用于身份验证和授权

### session和Cookie 有什么区别

1. 存储位置：Session 对象存储在服务器端，而 Cookie 存储在客户端（浏览器）
2. 数据存储：Session 对象可以存储较大量的数据，通常以键值对的形式保存在服务器的内存或持久化存储中；而 Cookie 的存储容量有限，通常只能存储少量文本数据（4KB左右）。
3. 安全性：由于 Session 对象存储在服务器端，相对于 Cookie 更安全，因为客户端无法直接修改 Session 数据。Cookie 存储在客户端，容易受到篡改和伪造的风险。
4. 生命周期：Session 对象的生命周期由服务器管理，可以设置过期时间或依赖用户会话；而 Cookie 可以设置过期时间，也可以设置为会话 Cookie，在关闭浏览器后自动删除。

### 如何实现token

#### 导入依赖

```
   <!--        jwt 依赖 -->
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
            <version>0.9.1</version>
        </dependency>

        <dependency>
            <groupId>com.auth0</groupId>
            <artifactId>java-jwt</artifactId>
            <version>3.4.0</version>
        </dependency>
```

### 创建jwt工具类

```
package com.shanhui.util;







import com.auth0.jwt.JWT;
import com.auth0.jwt.JWTCreator;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.interfaces.Claim;
import com.auth0.jwt.interfaces.DecodedJWT;
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.JwtBuilder;
import io.jsonwebtoken.Jwts;

import java.time.*;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;

public class JwtUtil {


    // token签名加密密钥
    private static final String  secret = "#cai*cai%Vc";

    /**
     * 创建token
     * @param map
     * @return
     */
    public static String createAccessToken(Map<String,String> map){
        JWTCreator.Builder builder = JWT.create();
        // 给签名添加参数
        map.forEach((k,v)->{
            builder.withClaim(k,v);
        });
        //设置token过期时间
        builder.withExpiresAt(new Date(System.currentTimeMillis()+40*60*1000));
        //设置token创建时间
        builder.withIssuedAt(new Date(System.currentTimeMillis()));
        return  builder.sign(Algorithm.HMAC256(secret));
    }


    /**
     * 判断是否可以刷新token
     * @param token
     * @return
     */
    public static Boolean canToken(String token){

        DecodedJWT decode = JWT.decode(token);
        // 获取token的结束时间
        Date expiresAt = decode.getExpiresAt();

        // 时间转换成LocalDateTime
        Instant instant = expiresAt.toInstant();
        ZoneId zoneId = ZoneId.systemDefault();
        LocalDateTime localDateTime = instant.atZone(zoneId).toLocalDateTime();
        System.out.println(LocalDateTime.now());
        // 计算当前时间离结束时间还有多少分钟
        Duration between = Duration.between(LocalDateTime.now(),localDateTime);
        // token过期时间是40分钟，如果过期时间大于30分钟，不用刷新token，小于30分钟刷新token
        if ((between.getSeconds()/60)>30&&(between.getSeconds()/60)<=0){
            return false;
        }
       return  true;
    }


    /**
     * 刷新token
     * @param token
     * @return
     */
    public static String refreshToken(String token){
        DecodedJWT decode = JWT.decode(token);
        String account = decode.getClaim("account").asString();
        String userId = decode.getClaim("userId").asString();
        Map<String,String> map = new HashMap<>();
        map.put("account",account);
        map.put("userId",userId);
        return createAccessToken(map);
    }

    /**
     * 获取token的参数
     * @param token
     * @return
     */
    public static Map<String,String>  getClaim(String token){
        DecodedJWT decode = JWT.decode(token);
        Map<String,String> map = new HashMap<>();
        String account = decode.getClaim("account").asString();
        String userId = decode.getClaim("userId").asString();
        map.put("account",account);
        map.put("userId",userId);
        return  map;
    }

    public static void main(String[] args) {
        Map<String,String> map = new HashMap<>();
        map.put("account","admin");
        map.put("userId","1");
        String accessToken = createAccessToken(map);
        System.out.println("token 创建成功"+accessToken);
        System.out.println(canToken(accessToken));
        Map<String, String> claim = getClaim(accessToken);
        System.out.println(claim.get("account"));
    }

}

```

