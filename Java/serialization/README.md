# Serialization

> ### references ๐
> Java์ ์ ์   

## Contents		
* ### [์์ถ๋ ฅ](https://github.com/mingeun2154/skill/tree/main/Java/serialization#i\/o)      
* ### [์คํธ๋ฆผ](https://github.com/mingeun2154/skill/tree/main/Java/serialization#stream)      
* ### [์ง๋ ฌํ](https://github.com/mingeun2154/skill/tree/main/Java/serialization#serialization-1)      
* ### [๊ฐ์ฒด](https://github.com/mingeun2154/skill/tree/main/Java/serialization#object)
* ### [ObjectInputStream๊ณผ ObjectOutputStream](https://github.com/mingeun2154/skill/tree/main/Java/serialization#objectinputstream-and-objectoutputstream)      
* ### [์ง๋ ฌํ ๊ฐ๋ฅํ ํด๋์ค](https://github.com/mingeun2154/skill/tree/main/Java/serialization#serializable)
* ### [์ง๋ ฌํ ๋์ ์ ์ธ](https://github.com/mingeun2154/skill/tree/main/Java/serialization#transient)      

#    

## I/O
์์ถ๋ ฅ์ ์ปดํจํฐ ๋ด๋ถ ๋๋ ์ธ๋ถ์ ์ฅ์น์ ํ๋ก๊ทธ๋จ ๊ฐ์ ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ ๋ฐ๋ ๊ฒ์ ๋งํ๋ค.

Disk์ ํ์ผ์ ์ผ๊ณ  ์ด๋ค๋๊ฐ, ํค๋ณด๋๋ก๋ถํฐ ๋ฐ์ดํฐ๋ฅผ ์๋ ฅ๋ฐ๊ฑฐ๋ ๋ชจ๋ํฐ๋ก ํ๋ฉด์ ์ถ๋ ฅํ๋ ๊ฒ ๋ชจ๋ ์์ถ๋ ฅ์ ์์ด๋ค.

## Stream
> stream์ ๋ฌผ์ ํ๋ฆ์ ์๋ฏธํ๋ ๋จ์ด์ด๋ค.

์คํธ๋ฆผ์ด๋ ๋ฐ์ดํฐ๋ฅผ ๊ตํํ๋ ค๋ ๋ ๋์์ ์ฐ๊ฒฐํ์ฌ **๋ฐ์ดํฐ๊ฐ ์ด๋ํ  ์ ์๋๋ก ํ๋ ํต๋ก**์ด๋ค. 

์คํธ๋ฆผ์ **๋จ๋ฐฉํฅ ํต์ ๋ง ๊ฐ๋ฅ**ํ๊ณ  ํ๋์ ์คํธ๋ฆผ์ผ๋ก ์๋ ฅ๊ณผ ์ถ๋ ฅ์ ๋์์ ์ฒ๋ฆฌ ํ  ์ ์๋ค. ๊ทธ๋์ ์์ถ๋ ฅ์ ๋์์ ์ํํ๋ ค๋ฉด ์คํธ๋ฆผ์ด ๋ ๊ฐ ํ์ํ๋ค.

## Serialization
์ง๋ ฌํ๋ **๊ฐ์ฒด๋ฅผ ๋ฐ์ดํฐ ์คํธ๋ฆผ**์ผ๋ก ๋ง๋๋ ๊ฒ์ ๋ปํ๋ค. ๊ฐ์ฒด์ ์ ์ฅ๋ ๋ฐ์ดํฐ๋ฅผ ์คํธ๋ฆผ์ ์ฐ๊ธฐ(write) ์ํด ์ฐ์์ ์ธ(serial) ๋ฐ์ดํฐ๋ก ๋ณํํ๋ ๊ฒ์ด๋ค.

๋ฐ๋๋ก ์คํธ๋ฆผ์ผ๋ก๋ถํฐ ๋ฐ์ดํฐ๋ฅผ ์ฝ์ด ๊ฐ์ฒด๋ฅผ ๋ง๋๋ ๊ฒ์ ์ญ์ง๋ ฌํ(deserialization)๋ผ๊ณ  ํ๋ค.

`ObjectInputStream`, `ObjectOutputStream`์ ์ฌ์ฉํ๋ค.

## Object
๊ฐ์ฒด๋ ํด๋์ค์ ์ ์๋ **์ธ์คํด์ค๋ณ์์ ์งํฉ**์ด๋ค. **static๋ณ์, ๋ฉ์๋๋ ํฌํจ๋์ง ์๋๋ค**. ๊ฐ์ฒด๋ ์ค์ง ์ธ์คํด์ค๋ณ์๋ค๋ก๋ง ๊ตฌ์ฑ๋๋ค.

์ธ์คํด์ค๋ณ์๋ ์ธ์คํด์ค๋ง๋ค ๋ณ๋์ ๊ฐ์ ๊ฐ์ง๊ธฐ ๋๋ฌธ์ ๋ณ๋์ ์ ์ฅ๊ณต๊ฐ์ด ํ์ํ์ง๋ง ๋ฉ์๋๋ ๊ทธ๋ ์ง ์๊ธฐ ๋๋ฌธ์ ์ธ์คํด์ค๋ง๋ค ๊ฐ์ ๋ด์ฉ์ ์ฝ๋๋ฅผ ํฌํจ์ํค์ง ์๋๋ค.

๊ฒฐ๊ตญ **๊ฐ์ฒด๋ฅผ ์ ์ฅํ๋ค๋ ๊ฒ์ ์ธ์คํด์ค๋ณ์๋ค์ ๊ฐ์ ์ ์ฅํ๋ค๋ ๊ฒ**์ด๋ค.
## `ObjectInputStream` and `ObjectOutputstream`
* ์ง๋ ฌํ(์คํธ๋ฆผ์ ๊ฐ์ฒด๋ฅผ **์ถ๋ ฅ**) : `ObjectOutputStream` ์ฌ์ฉ
* ์ญ์ง๋ ฌํ(์คํธ๋ฆผ์ผ๋ก๋ถํฐ ๊ฐ์ฒด๋ฅผ **์๋ ฅ**) : `ObjectInputStream` ์ฌ์ฉ

`ObjectInputStream`๊ณผ `ObjectOutputStream`์ **๋ณด์กฐ์คํธ๋ฆผ**์ด๊ธฐ ๋๋ฌธ์ ๊ธฐ๋ฐ์คํธ๋ฆผ์ด ํ์ํ๋ค.

์๋ฅผ ๋ค์ด ํ์ผ์ ๊ฐ์ฒด๋ฅผ ์ ์ฅ(์ง๋ ฌํ)ํ๊ณ  ์ถ๋ค๋ฉด ๋ค์๊ณผ ๊ฐ์ด ์ฝ๋๋ฅผ ์์ฑํ๋ค.
```Java
        try ( FileOutputStream fos = new FileOutputStream("objectfile.ser");
            ObjectOutputStream out = new ObjectOutputStream(fos);
        ) {
            out.writeObject(new UserInfo("mingeun", "password", 24)); // ์ญ์ง๋ ฌํ๋ readObject()
        } catch (IOException e) {
            System.out.println("IOException : " + e.getMessage());
            e.printStackTrace();
        }
```

* `fos` : ์ค์  ๋ฐ์ดํฐ๋ฅผ ์ถ๋ ฅํ๋ ๊ธฐ๋ฐ์คํธ๋ฆผ. objectfile.ser์ด๋ผ๋ ํ์ผ๊ณผ ์ฐ๊ฒฐ๋๋ค.
* `out` : ์ง๋ ฌํ์คํธ๋ฆผ
* `writeObject()` ํจ์๋ `IOException`์ ๋์ง๋ค.
* `readObject()` ํจ์๋ `IOException`, `ClassNotFoundException`์ ๋์ง๋ฉฐ `Object` ํ์์ ๋ฐํํ๊ธฐ ๋๋ฌธ์ **ํ ๋ณํ**์ ํด์ค์ผ ํ๋ค.

## Serializable

์ง๋ ฌํ ๋๋ ์ญ์ง๋ ฌํ์ ๋์์ด ๋๋ ํด๋์ค๋ **Serializable ์ธํฐํ์ด์ค**๋ฅผ ๊ตฌํํด์ผ ํ๋ค.
> ๊ทธ๋ ์ง ์์ผ๋ฉด `java.io.NotSerializableException` ์ด ๋ฐ์ํ๋ค.

```Java
public class SuperUserInfo {
	String name;
	String password;
}

public class UserInfo extends SuperUserInfo implements Serializable {
	int age;
}
```

`Serializable`์ ๊ตฌํํ `UserInfo`๋ ์ง๋ ฌํ๋์ง๋ง, ๊ทธ๋ ์ง ์์ `SuperUserInfo`์ ์ ์๋ `name`๊ณผ `password`๋ **์ง๋ ฌํ ๋์์์ ์ ์ธ**๋๋ค.

`Object` ํด๋์ค๋ `Serializable`์ ๊ตฌํํ์ง ์์๊ธฐ ๋๋ฌธ์ ์ง๋ ฌํํ  ์ ์๋ค.

```Java
public class UserInfo implements Serializable {
	String name;
	String password;
	int age;

	Object obj1 = new Object();	// ์ง๋ ฌํ ๋ถ๊ฐ๋ฅ
	Object obj2 = new String("obj");	// ์ง๋ ฌํ ๊ฐ๋ฅ
}
```

> ์ง๋ ฌํ ๊ฐ๋ฅ ์ฌ๋ถ๋ ์ธ์คํด์ค๋ณ์์ ํ์์ด ์๋ **์ค์ ๋ก ์ฐธ์กฐ๋๋ ๊ฐ์ฒด์ ์ข๋ฅ**์ ์ํด ๊ฒฐ์ ๋๋ค.

## transient
์ง๋ ฌํํ๊ณ ์ ํ๋ ๊ฐ์ฒด์ ํด๋์ค์ ์ง๋ ฌํ๊ฐ ์ ๋๋ ๊ฐ์ฒด์ ๋ํ ์ฐธ์กฐ๋ฅผ ํฌํจํ๊ณ  ์์ผ๋ฉด `java.io.NotSerializableException`์ด ๋ฐ์ํ๋ค.

`transient` ํค์๋๋ฅผ ์ฌ์ฉํด ํด๊ฒฐํ  ์ ์๋ค. ์ด ํค์๋๊ฐ ๋ถ์ ๋์์ **์ง๋ ฌํ ๋์์์ ์ ์ธ**๋๋ค.

๋๋ ๋ณด์์ ์ง๋ ฌํ๋๋ฉด ์ ๋๋ ๊ฐ(password ๋ฑ)์ ๋ํด์๋ `transient`๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
> `transient`๊ฐ ๋ถ์ ์ธ์คํด์ค๋ณ์์ ๊ฐ์ ๊ทธ ํ์์ ๊ธฐ๋ณธ๊ฐ์ผ๋ก ์ง๋ ฌํ ๋๋ค.

```Java
public class UserInfo implements Serializable {
	String name;
	transient String password;	// ์ง๋ ฌํ ๋์์์ ์ ์ธ๋๋ค.
	int age;

	transient Object obj = new Object();	// ์ง๋ ฌํ ๋์์์ ์ ์ธ๋๋ค.
}
```

> UserInfo ๊ฐ์ฒด๋ฅผ ์ญ์ง๋ ฌํํ๋ฉด ์ฐธ์กฐ๋ณ์์ธ obj์ password์ ๊ฐ์ null์ด ๋๋ค.
