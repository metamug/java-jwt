# java-jwt
Java implementation of JSON Web Token (JWT) 


## Usage


### Generate JWT Token 

The following code can be used to generate JWT token

```java

private static final int EXPIRY_DAYS = 90;

JSONObject jwtPayload = new JSONObject();
jwtPayload.put("status", 0);

JSONArray audArray = new JSONArray();
audArray.put("admin"); 
jwtPayload.put("sub", "John");

jwtPayload.put("aud", audArray);
LocalDateTime ldt = LocalDateTime.now().plusDays(EXPIRY_DAYS);
jwtPayload.put("exp", ldt.toEpochSecond(ZoneOffset.UTC)); //this needs to be configured
        
String token = new JWebToken(jwtPayload).toString();
```

### Verify JWT Token 

JWT token recieved in the String format can be used to verify and extract audience and subject information as follows.

```java
//verify and use
JWebToken incomingToken = new JWebToken(bearerToken);
if (!incomingToken.isValid()) {
    String audience = incomingToken.getAudience();
    String subject = incomingToken.getSubject();
}
```

### JWT Tutorial 

https://metamug.com/article/security/jwt-java-tutorial-create-verify.html
