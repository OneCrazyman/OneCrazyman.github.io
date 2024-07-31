---
title: "[Data Structure] heap과 stack메모리"
date: '2024-06-10'
---
## 메모리
메모리 관리는 프로그램에 있어 성능과 안정성에 큰 영향을 끼친다. 코드를 실행하려면 메모리에서 해당 코드를 읽어야하고, 코드에서 필요한 데이터들을 메모리에서 가져와야한다. 이에 따라 메모리를 여러 영역으로 나누고 각기 다른 방법을 통해 각 영역에 접근을 하게 된다.

### 메모리 영역

|         |
|-----------------|
| 힙 영역         |
| 스택 영역       |
| 코드 영역       |

### 스택 메모리

- 주로 정적 메모리를 할당하는 영역이며, 함수 호출시 자동으로 호출되고, 함수 종료시 자동으로 해제되는 특징이 있다. 이를 컴파일러가 관리한다.
- 관리가 자동적으로 이루어지기 때문에 메모리 누수가 일어나지 않음
- 메모리 크기를 한번에 먹기 때문에, 많은 메모리 블록을 한번에 할당이 불가능하고, 함수 호출 깊이에 따라 스택 오버플로우가 발생할 수 있다.

- __스택이라 불리는 이유__
	- 
	```cpp
	void fun_1(){
		int x;
		int y;
	}

	void fun_2(){
		int a;
		int b;
		fun_1();
	}

	int main(){
		fun_2()
		return 0;
	}
	```
	위와 같은 코드가 있을때 메모리와 스택 메모리에서 어떤 일이 벌어질지 보자

	우선 코드 영역에서 코드를 읽어 메인 함수를 호출하고 fun_2()를 호출하며 stack에 올린다.
	
	### 스택 메모리 영역

| **함수 호출** | **변수** | **설명**                |
|---------------|----------|-------------------------|
| `main`        |          | `main` 함수의 스택 프레임 생성 |
|               |          | `fun_2` 함수 호출        |
| `fun_2`       | `a`      | `fun_2` 함수의 스택 프레임에 할당된 지역 변수 `a` |
|               | `b`      | `fun_2` 함수의 스택 프레임에 할당된 지역 변수 `b` |
|               |          | `fun_1` 함수 호출        |
| `fun_1`       | `x`      | `fun_1` 함수의 스택 프레임에 할당된 지역 변수 `x` |
|               | `y`      | `fun_1` 함수의 스택 프레임에 할당된 지역 변수 `y` |
|               |          | `fun_1` 함수 종료, 스택 프레임 해제 |
| `fun_2`       |          | `fun_2` 함수 종료, 스택 프레임 해제 |
| `main`        |          | `main` 함수 종료, 스택 프레임 해제 |

	fun_1이 가장 늦게 호출 되었지만, 가장 먼저 종료되었다. LIFO의 형식을 따르는 메모리 영역이기에 stack메모리 영역이라고 부른다.

### 힙 메모리
- 주로 동적 메모리 할당 영역으로, 코더의 필요에 따라 할당하고 해제한다.
- `malloc`, `free` (C 언어), `new`, `delete` (C++) 등을 사용하여 프로그래머가 직접 관리.
- 포인터를 사용해서 접근한다. 스택 영역에 포인터 변수를 할당하고 힙 메모리에 동적메모리를 할당하여 사용.

## 힙과 스택 메모리의 차이


| **Parameter**               | **STACK**                                                   | **HEAP**                                               |
|-----------------------------|-------------------------------------------------------------|--------------------------------------------------------|
| **Basic**                   | 메모리는 연속된 블록으로 할당됨                                 | 메모리는 임의의 순서로 할당됨                                  |
| **Allocation and De-allocation** | 컴파일러 지시에 의해 자동으로 할당 및 해제                        | 프로그래머에 의해 수동으로 할당 및 해제                           |
| **Cost**                    | 적음                                                        | 많음                                                   |
| **Implementation**          | 쉬움                                                        | 어려움                                                 |
| **Access time**             | 더 빠름                                                      | 더 느림                                                 |
| **Main Issue**              | 메모리 부족                                                  | 메모리 단편화                                            |
| **Locality of reference**   | 훌륭함                                                      | 적당함                                                  |
| **Safety**                  | 스레드 안전, 저장된 데이터는 소유자만 접근 가능                    | 스레드 안전하지 않음, 저장된 데이터는 모든 스레드에 노출됨               |
| **Flexibility**             | 고정 크기                                                    | 크기 조절 가능                                            |
| **Data type structure**     | 선형 구조                                                    | 계층 구조                                                |
| **Preferred**               | 배열에서는 스택 메모리 할당이 선호됨                              | 연결 리스트에서는 힙 메모리 할당이 선호됨                        |
| **Size**                    | 힙 메모리보다 작음                                             | 스택 메모리보다 큼                                          |
