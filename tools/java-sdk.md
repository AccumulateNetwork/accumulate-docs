---
description: Accumulate Java SDK Guide
---

# Java SDK

The Accumulate SDK is a Java library for implementing sending and receiving tokens in Java apps with Accumulate. It provides easy-to-use Java methods, and Integrating our SDK into your Desktop application is easy and beginner-friendly.&#x20;

Accumulate Java SDK helps the developers to integrate their applications with Accumulate network. It has ready-made methods to execute. So, the developers can reuse the codebase and develop their applications efficiently.&#x20;

To view the Java generated documentation, visit this [link](https://arsrtech.github.io/accumulate-java-sdk/doc/com/sdk/accumulate/service/Client.html)

Requirements:&#x20;

* Basic Java programming language experience&#x20;
* Java 11+&#x20;
* IntelliJ Idea IDE&#x20;
* Maven installed ([https://www.jetbrains.com/help/idea/convert-a-regular-project-into-a-maven-project.html](https://www.jetbrains.com/help/idea/convert-a-regular-project-into-a-maven-project.html))&#x20;
* Basic knowledge of Accumulate &#x20;

In this guide, we focused on two main parts, the Installation and code examples of the Java SDK.&#x20;

{% hint style="info" %}
This tutorial uses IntelliJ&#x20;
{% endhint %}

### **Installation**&#x20;

**Add pom.xml file** &#x20;

1. Open an existing Java project&#x20;
2. In the Project tool window, right-click your project and select Add Framework Support.&#x20;

![](<../.gitbook/assets/Screenshot 2022-05-17 at 13.56.21.png>)

3\. In the open dialog, select Maven from the options on the left and click OK.

![](<../.gitbook/assets/Screenshot 2022-05-17 at 13.58.17.png>)

IntelliJ IDEA will automatically add a pom.xml file to the project and generates the standard Maven layout in the Project tool window.

![](<../.gitbook/assets/Screenshot 2022-05-17 at 14.01.28.png>)

Open the generated pom.xml file and add the below information. The artifactId and version are specified automatically.

```
<?xml version="1.0" encoding="UTF-8"?> 

<project xmlns="http://maven.apache.org/POM/4.0.0" 

         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"> 

    <modelVersion>4.0.0</modelVersion> 

  

    <groupId>org.example</groupId> 

    <artifactId>test-project</artifactId> 

    <version>1.0-SNAPSHOT</version> 

    <repositories> 

        <repository> 

            <id>com.sdk.accumulate</id> 

            <url>http://18.232.151.167:8082/artifactory/libs-release-local/</url> 

        </repository> 

    </repositories> 

    <properties> 

        <maven.compiler.source>11</maven.compiler.source> 

        <maven.compiler.target>11</maven.compiler.target> 

    </properties> 

    <dependencies> 

    <dependency> 

        <groupId>com.sdk.accumulate</groupId> 

        <artifactId>AccumulateJavaSDK</artifactId> 

        <version>1.1</version> 

    </dependency> 

    <dependency> 

        <groupId>org.purejava</groupId> 

        <artifactId>tweetnacl-java</artifactId> 

        <version>1.1.2</version> 

    </dependency> 

    <dependency> 

        <groupId>org.apache.commons</groupId> 

        <artifactId>commons-lang3</artifactId> 

        <version>3.12.0</version> 

    </dependency> 

    <dependency> 

        <groupId>com.fasterxml.jackson.core</groupId> 

        <artifactId>jackson-databind</artifactId> 

        <version>2.13.2.1</version> 

    </dependency> 

    <dependency> 

        <groupId>org.apache.httpcomponents</groupId> 

        <artifactId>httpclient</artifactId> 

        <version>4.5.13</version> 

    </dependency> 

    </dependencies> 

</project> 
```

### **Configure the Java SDK repo (settings.xml configuration)**&#x20;

* Currently, the Java SDK is hosted in a private repository. To access the repository we have to specify the username and password of the repository.&#x20;
* To set the credentials, we have to create a settings file inside the `.m2` directory.&#x20;
* Since we are using the maven, the system itself can create the `.m2` directory while maven installation.&#x20;
* Else follow the below steps.&#x20;
* `$ cd` - It will go to the home directory. (for example /home/user/)&#x20;
* `$ mkdir .m2` - It will create a `.m2` directory (/home/user/.m2/)&#x20;
* Now create a settings.xml file inside the `.m2` directory (/home/user/.m2/settings.xml)&#x20;
* Then paste the below xml content into the `settings.xml` file.

```
<?xml version="1.0" encoding="UTF-8"?> 
<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 http://maven.apache.org/xsd/settings-1.2.0.xsd" xmlns="http://maven.apache.org/SETTINGS/1.2.0" 
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
    <servers> 
        <server> 
            <username>admin</username> 
            <password>Admin@123</password> 
            <id>com.sdk.accumulate</id> 
        </server> 
    </servers> 
    <mirrors> 
        <mirror> 
            <id>insecure-repo</id> 
            <mirrorOf>external:http:*</mirrorOf> 
            <url>http://18.232.151.167:8082/artifactory/libs-release-local/</url> 
            <blocked>false</blocked> 
        </mirror> 
    </mirrors> 
</settings> 
 
```

* And save the file&#x20;
* Now the system can access the Java SDK private repository.&#x20;

Now you have your project fully configured to use the Accumulate Java SDK. We have some code examples below to help you get started using the SDK to make it easier.&#x20;

### **Code Reference** &#x20;

The Accumulate java SDK methods with examples of how to use them in your project.&#x20;

**LiteAccount**&#x20;

```
public class LiteAccount{ 
    public static void main(String[] args) throws Exception { 
 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
    System.out.println("response" + " " + liteAccount); 
 
    } 
} 
```

**Faucet**

```
public class Faucet{ 
    public static void main(String[] args) throws Exception { 
 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 

       String faucet = client.getFaucet(liteAccount.url().string()); 

    System.out.println("response" + " " + faucet); 
 
 
    } 
} 
```

**Add Credit**

```
public class AddCredit { 
    public static void main(String[] args) throws Exception { 
 
            TestNetClient client = new TestNetClient(); 
            LiteAccount liteAccount = LiteAccount.generate(); 
            String response = client.getFaucet(liteAccount.url().string()); 
            System.out.println("Lite Account Response: "+response); 
 
            AddCreditsArg addCreditsArg = new AddCreditsArg(); 
            addCreditsArg.setAmount(1000); 
            addCreditsArg.setRecipient(liteAccount.url().string()); 
            String addCreditsResponse = client.addCredits(addCreditsArg,liteAccount); 
            System.out.println("Add Credits Response: "+addCreditsResponse); 
 
    } 
} 
```

**BurnTokens**

```
public class BurnTokens { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        BurnTokensArg burnTokensArg = new BurnTokensArg(); 
        burnTokensArg.setAmount(BigInteger.valueOf(56879)); 
        String burnTokensResponse = client.burnTokens(burnTokensArg,liteAccount); 
        System.out.println("Burn token Response: "+burnTokensResponse); 
    } 
} 
```

**CreateADI**

```
public class CreateADI { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl("acc://my-own-identity"); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
    } 
} 
```

**CreateDataAccount**

```
public class CreateDataAccount { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
 
        String identityUrl = "acc://my-own-identity-1"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl),kp); 
 
        CreateDataAccountArg createDataAccountArg = new CreateDataAccountArg(); 
        createDataAccountArg.setUrl(identityUrl+"/data"); 
        createDataAccountArg.setKeyBookUrl(identityUrl+"/test-key-book"); 
        createDataAccountArg.setManagerKeyBookUrl(identityUrl+"/test-key-book"); 
        createDataAccountArg.setScratch(true); 
        String createDataAccountResponse = client.createDataAccount(createDataAccountArg,adi); 
        System.out.println("Create data account Response: "+createDataAccountResponse); 
    } 
} 
```

**CreateKeyBook**

```
public class CreateKeyBook { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        String identityUrl = "acc://my-own-identity-1"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl),kp); 
 
        CreateKeyBookArg createKeyBookArg = new CreateKeyBookArg(); 
        createKeyBookArg.setUrl(identityUrl+"/book1"); 
        List<String> pages = new ArrayList<>(); 
        pages.add(identityUrl+"/test-key-page"); 
        createKeyBookArg.setPages(pages); 
        String createKeyBook = client.createKeyBook(createKeyBookArg,adi); 
        System.out.println("Create Key book Response: "+createKeyBook); 
    } 
} 
```

**CreateKeyPage**

```
public class CreateKeyPage { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        String identityUrl = "acc://my-own-identity-1"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl),kp); 
 
        CreateKeyPageArg createKeyPageArg = new CreateKeyPageArg(); 
        List<byte[]> keys = new ArrayList<>(); 
        keys.add(liteAccount.getPublicKey()); 
        createKeyPageArg.setKeys(keys); 
        createKeyPageArg.setUrl(identityUrl+"/test-key-page"); 
        String createKeyPageResponse = client.createKeyPage(createKeyPageArg,adi); 
        System.out.println("Create Key page Response: "+createKeyPageResponse); 
    } 
} 
 
```

**CreatToken**

```
public class CreateToken { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        AddCreditsArg addCreditsArg = new AddCreditsArg(); 
        addCreditsArg.setAmount(500000); 
        addCreditsArg.setRecipient(liteAccount.url().string()); 
        String addCreditsResponse = client.addCredits(addCreditsArg,liteAccount); 
        System.out.println("Add Credits Response: "+addCreditsResponse); 
 
        String identityUrl = "acc://my-own-identity-3"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
        Thread.sleep(5000); 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl),kp); 
 
        CreateTokenArg createTokenArg = new CreateTokenArg(); 
        createTokenArg.setUrl(identityUrl+"/tok"); 
        createTokenArg.setKeyBookUrl(identityUrl+"/test-key-page"); 
        createTokenArg.setSymbol("INR"); 
        createTokenArg.setPrecision(10); 
        createTokenArg.setProperties("acc://my-own-identity-3/INR"); 
        createTokenArg.setInitialSupply(BigInteger.valueOf(1000000000)); 
        createTokenArg.setHasSupplyLimit(true); 
        createTokenArg.setManager("acc://my-own-identity-3/test-key-page"); 
        String createTokenResponse = client.createToken(createTokenArg,adi); 
        System.out.println("Create Token Response: "+createTokenResponse); 
    } 
}
```

**CreatTokenAccount**

```
public class CreateTokenAccount { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: " + response); 
 
        String identityUrl = "acc://my-own-identity-2"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg, liteAccount); 
        System.out.println("Create ADI Response: " + createAdiResponse); 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl), kp); 
 
        CreateTokenAccountArg createTokenAccountArg = new CreateTokenAccountArg(); 
        createTokenAccountArg.setUrl(identityUrl); 
        createTokenAccountArg.setTokenUrl(identityUrl + "/tok"); 
        createTokenAccountArg.setKeyBookUrl(identityUrl + "/test-key-book"); 
        createTokenAccountArg.setScratch(true); 
        String createTokenAccountResponse = client.createTokenAccount(createTokenAccountArg, adi); 
        System.out.println("Create Token Account Response: " + createTokenAccountResponse); 
    } 
}
```

**IssueToken**

```
public class IssueToken { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        LiteAccount liteAccount2 = LiteAccount.generate(); 
        String response2 = client.getFaucet(liteAccount2.url().string()); 
        System.out.println("Lite Account Response: "+response2); 
 
        IssueTokensArg issueTokensArg = new IssueTokensArg(); 
        issueTokensArg.setRecipient(liteAccount2.url().string()); 
        issueTokensArg.setAmount(1); 
        String issueTokensResponse = client.issueTokens(issueTokensArg,liteAccount); 
        System.out.println("Issue Token  Response: "+issueTokensResponse); 
    } 
} 
```

**SendToken**

```
public class SendToken { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        LiteAccount liteAccount2 = LiteAccount.generate(); 
        String response2 = client.getFaucet(liteAccount2.url().string()); 
        System.out.println("Lite Account Response: "+response2); 
 
        SendTokensArg sendTokensArg = new SendTokensArg(); 
        List<TokenRecipientArg> to = new ArrayList<>(); 
        TokenRecipientArg tokenRecipientArg = new TokenRecipientArg(); 
        tokenRecipientArg.setAmount(20000000); 
        tokenRecipientArg.setUrl(liteAccount2.url().string()); 
        to.add(tokenRecipientArg); 
        sendTokensArg.setTo(to); 
        String sendTokensResponse = client.sendToken(sendTokensArg,liteAccount); 
        System.out.println("Send Token  Response: "+sendTokensResponse); 
    } 
}
```

**UpdateKeyPage**

```
public class UpdateKeyPage { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl("acc://my-own-identity"); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
 
        UpdateKeyPageArg updateKeyPageArg = new UpdateKeyPageArg(); 
        updateKeyPageArg.setOwner("acc://my-own-identity"); 
        TweetNaclFast.Signature.KeyPair kp1 = TweetNaclFast.Signature.keyPair(); 
        updateKeyPageArg.setNewKey(kp1.getPublicKey()); 
        updateKeyPageArg.setKey(kp.getPublicKey()); 
        updateKeyPageArg.setOperation(KeyPageOperation.UpdateKey); 
        String updateKeyPageResponse = client.updateKeyPage(updateKeyPageArg,liteAccount); 
        System.out.println("update KeyPage Response  Response: "+updateKeyPageResponse); 
    } 
}
```

**WriteData**

```
public class WriteData { 
    public static void main(String[] args) throws Exception { 
        TestNetClient client = new TestNetClient(); 
        LiteAccount liteAccount = LiteAccount.generate(); 
        String response = client.getFaucet(liteAccount.url().string()); 
        System.out.println("Lite Account Response: "+response); 
 
        String identityUrl = "acc://my-own-identity-1"; 
        CreateIdentityArg createIdentityArg = new CreateIdentityArg(); 
        createIdentityArg.setUrl(identityUrl); 
        TweetNaclFast.Signature.KeyPair kp = TweetNaclFast.Signature.keyPair(); 
        createIdentityArg.setPublicKey(kp.getPublicKey()); 
        createIdentityArg.setKeyBookName("test-key-book"); 
        createIdentityArg.setKeyPageName("test-key-page"); 
        String createAdiResponse = client.createIdentity(createIdentityArg,liteAccount); 
        System.out.println("Create ADI Response: "+createAdiResponse); 
        ADI adi = new ADI(AccURL.toAccURL(identityUrl),kp); 
 
        WriteDataArg writeDataArg = new WriteDataArg(); 
        writeDataArg.setData("Test".getBytes(StandardCharsets.UTF_8)); 
        List<byte[]> bytes = new ArrayList<>(); 
        bytes.add(new byte[0]); 
        writeDataArg.setExtIds(bytes); 
        String writeDataResponse = client.writeData(writeDataArg,adi); 
        System.out.println("Write data Response  Response: "+writeDataResponse); 
    } 
} 
```

****
