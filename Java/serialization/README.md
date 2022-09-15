# Serialization

> ### references 🔗
> Java의 정석   

## Contents		
* ### [입출력](https://github.com/mingeun2154/skill/tree/main/Java/serialization#i\/o)      
* ### [스트림](https://github.com/mingeun2154/skill/tree/main/Java/serialization#stream)      
* ### [직렬화](https://github.com/mingeun2154/skill/tree/main/Java/serialization#serialization-1)      
* ### [객체](https://github.com/mingeun2154/skill/tree/main/Java/serialization#object)
* ### [ObjectInputStream과 ObjectOutputStream](https://github.com/mingeun2154/skill/tree/main/Java/serialization#objectinputstream-and-objectoutputstream)      
* ### [직렬화 가능한 클래스](https://github.com/mingeun2154/skill/tree/main/Java/serialization#serializable)
* ### [직렬화 대상 제외](https://github.com/mingeun2154/skill/tree/main/Java/serialization#transient)      

#    

## I/O
입출력은 컴퓨터 내부 또는 외부의 장치와 프로그램 간의 데이터를 주고받는 것을 말한다.

Disk에 파일을 일고 쓴다던가, 키보드로부터 데이터를 입력받거나 모니터로 화면에 출력하는 것 모두 입출력의 예이다.

## Stream
> stream은 물의 흐름을 의미하는 단어이다.

스트림이란 데이터를 교환하려는 두 대상을 연결하여 **데이터가 이동할 수 있도록 하는 통로**이다. 

스트림은 **단방향 통신만 가능**하고 하나의 스트림으로 입력과 출력을 동시에 처리 할 수 없다. 그래서 입출력을 동시에 수행하려면 스트림이 두 개 필요하다.

## Serialization
직렬화란 **객체를 데이터 스트림**으로 만드는 것을 뜻한다. 객체에 저장된 데이터를 스트림에 쓰기(write) 위해 연속적인(serial) 데이터로 변환하는 것이다.

반대로 스트림으로부터 데이터를 읽어 객체를 만드는 것을 역직렬화(deserialization)라고 한다.

`ObjectInputStream`, `ObjectOutputStream`을 사용한다.

## Object
객체는 클래스에 정의된 **인스턴스변수의 집합**이다. **static변수, 메서드는 포함되지 않는다**. 객체는 오직 인스턴스변수들로만 구성된다.

인스턴스변수는 인스턴스마다 별도의 값을 가지기 때문에 별도의 저장공간이 필요하지만 메서드는 그렇지 않기 때문에 인스턴스마다 같은 내용의 코드를 포함시키지 않는다.

결국 **객체를 저장한다는 것은 인스턴스변수들의 값을 저장한다는 것**이다.
## `ObjectInputStream` and `ObjectOutputstream`
* 직렬화(스트림에 객체를 **출력**) : `ObjectOutputStream` 사용
* 역직렬화(스트림으로부터 객체를 **입력**) : `ObjectInputStream` 사용

`ObjectInputStream`과 `ObjectOutputStream`은 **보조스트림**이기 때문에 기반스트림이 필요하다.

예를 들어 파일에 객체를 저장(직렬화)하고 싶다면 다음과 같이 코드를 작성한다.
```Java
        try ( FileOutputStream fos = new FileOutputStream("objectfile.ser");
            ObjectOutputStream out = new ObjectOutputStream(fos);
        ) {
            out.writeObject(new UserInfo("mingeun", "password", 24)); // 역직렬화는 readObject()
        } catch (IOException e) {
            System.out.println("IOException : " + e.getMessage());
            e.printStackTrace();
        }
```

* `fos` : 실제 데이터를 출력하는 기반스트림. objectfile.ser이라는 파일과 연결된다.
* `out` : 직렬화스트림
* `writeObject()` 함수는 `IOException`을 던진다.
* `readObject()` 함수는 `IOException`, `ClassNotFoundException`을 던지며 `Object` 타입을 반환하기 때문에 **형 변환**을 해줘야 한다.

## Serializable

직렬화 또는 역직렬화의 대상이 되는 클래스는 **Serializable 인터페이스**를 구현해야 한다.
> 그렇지 않으면 `java.io.NotSerializableException` 이 발생한다.

```Java
public class SuperUserInfo {
	String name;
	String password;
}

public class UserInfo extends SuperUserInfo implements Serializable {
	int age;
}
```

`Serializable`을 구현한 `UserInfo`는 직렬화되지만, 그렇지 않은 `SuperUserInfo`에 정의된 `name`과 `password`는 **직렬화 대상에서 제외**된다.

`Object` 클래스는 `Serializable`을 구현하지 않았기 때문에 직렬화할 수 없다.

```Java
public class UserInfo implements Serializable {
	String name;
	String password;
	int age;

	Object obj1 = new Object();	// 직렬화 불가능
	Object obj2 = new String("obj");	// 직렬화 가능
}
```

> 직렬화 가능 여부는 인스턴스변수의 타입이 아닌 **실제로 참조되는 객체의 종류**에 의해 결정된다.

## transient
직렬화하고자 하는 객체의 클래스에 직렬화가 안 되는 객체에 대한 참조를 포함하고 있으면 `java.io.NotSerializableException`이 발생한다.

`transient` 키워드를 사용해 해결할 수 있다. 이 키워드가 붙은 대상은 **직렬화 대상에서 제외**된다.

또는 보안상 직렬화되면 안 되는 값(password 등)에 대해서도 `transient`를 사용할 수 있다.
> `transient`가 붙은 인스턴스변수의 값은 그 타입의 기본값으로 직렬화 된다.

```Java
public class UserInfo implements Serializable {
	String name;
	transient String password;	// 직렬화 대상에서 제외된다.
	int age;

	transient Object obj = new Object();	// 직렬화 대상에서 제외된다.
}
```

> UserInfo 객체를 역직렬화하면 참조변수인 obj와 password의 값은 null이 된다.
