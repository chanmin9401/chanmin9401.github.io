---

title: '[JAVA] TIME 패키지 활용법!'

excerpt: "TIME 패키지 소개 및 활용법"

categories:

- JAVA

tag:

- JAVA
- 실무활용
- 면접대비

author\_profile: true    #작성자 프로필 출력 여부

last\_modified\_at: 2022-02-04 T19:00:00+09:00

toc: true   #Table Of Contents 목차

toc\_sticky: true

\---

\## ⏰ TIME 패키지의 탄생 배경

기존에 사용된 Date, Calendar 패키지는 아래와 같은 단점 및 문제점들이 있습니다.

1. Calendar 인스턴스는 불변 객체가 아니라서 값이 수정될 수 있음.
1. 윤초와 같은 특수 케이스는 개별구현이 필요.
1. Calendar 클래스에서는 월을 나타낼 때 1월부터 12월을 0부터 11까지로 표현해야함.<br>

그러나 요일을 표시할 때는 1부터 7까지로 표현하는 등 일관적이지 못함.

그래서 많은 자바 개발자들은 Calendar 클래스뿐만 아니라 더 나은 성능의 Joda-Time이라는 라이브러리를 함께 사용해왔고,

JAVA SE 8 버전부터 Joda-Time 라이브러리를 발전시킨 새로운 날짜와 시간 API인 java.time 패키지를 제공하기 시작하였습니다.

\## 💻 TIME 패키지의 구성 클래스

기존의 Calendar 클래스는 날짜와 시간을 한 번에 표현했지만, TIME 패키지에서는 이를 구분하여 처리할 수 있습니다.

\### LocalDate, LocalTime

LocalDate 클래스는 날짜를 표현하는 데 사용되며, LocalTime 클래스는 시간을 표현하는 데 사용됩니다.

java.time 패키지에 포함된 대부분의 클래스들은 이 두 클래스를 확장한 것이 많으므로, 우선 이 두 클래스를 잘 이해하는 것이 중요합니다.

LocalDate와 LocalTime 클래스는 객체를 생성하기 위해서 now()와 of() 메소드라는 클래스 메소드를 제공합니다.<br>

|Method|Desc|

\|------|----|

|now()|현재의 날짜와 시간을 이용하여 새로운 객체를 생성하여 반환|

|of()|전달된 인수를 가지고 특정 날짜와 시간을 표현하는 새로운 객체를 생성하여 반환|

\```java

LocalDate today = LocalDate.now();

LocalTime present = LocalTime.now();

// static LocalDate of(int year, int month, int dayOfMonth)에 알맞는 인자를 전달하여 특정 날짜 생성

LocalDate birthDay = LocalDate.of(1994, 01, 04);

// static LocalTime of(int hour, int minute, int second, int nanoOfSecond)에 알맞는 인자를 전달하여 특정 시간을 생성

LocalTime birthTime = LocalTime.of(12, 13, 25, 123456789);

\```

\> \*\*of()\*\* 메소드는 다양한 형태가 오버로딩되어 제공

\### TemporalField Interface

TemporalField Interface는 날짜와 시간과 관련된 필드를 정의해 놓은 Interface입니다.

이를 구현하여 날짜와 시간을 나타낼 때 사용하는 열거체가 \*\*ChronoField\*\*이며,

java.time 패키지를 구성하는 클래스의 메소드에서는 이 \*\*ChronoField\*\*를 이용하여 날짜와 시간을 처리할 수 있습니다.

|Field|Desc|

\|------|----|

|YEAR|연도|

|MONTH\_OF\_YEAR|월|

|DAY\_OF\_MONTH|일|

|DAY\_OF\_WEEK|요일 (월요일:1, 화요일:2, ..., 일요일:7)|

|AMPM\_OF\_DAY|오전/오후|

|HOUR\_OF\_DAY|시(0~23)|

|CLOCK\_HOUR\_OF\_DAY|시(1~24)|

|HOUR\_OF\_AMPM|시(0~11)|

|CLOCK\_HOUR\_OF\_AMPM|시(1~12)|

|MINUTE\_OF\_HOUR|분|

|SECOND\_OF\_MINUTE|초|

|DAY\_OF\_YEAR|해당 연도의 몇 번째 날|

\### LocalDate - getter

|Method|Desc|

\|------|----|

|int get(TemporalField field)<br>long getLong(TemporalField field)|해당 날짜 객체의 명시된 필드의 값을 int형이나 long형으로 반환|

|int getYear()|해당 날짜 객체의 연도(YEAR) 필드의 값을 반환|

|Month getMonth()|해당 날짜 객체의 월(MONTH\_OF\_YEAR) 필드의 값을 Month 열거체를 이용하여 반환|

|int getMonthValue()|해당 날짜 객체의 월(MONTH\_OF\_YEAR) 필드의 값을 반환 (1~12)|

|int getDayOfMonth()|해당 날짜 객체의 일(DAY\_OF\_MONTH) 필드의 값을 반환 (1~31)|

|int getDayOfYear()|해당 날짜 객체의 일(DAY\_OF\_YEAR) 필드의 값을 반환|

|DayOfWeek getDayOfWeek()|해당 날짜 객체의 요일(DAY\_OF\_WEEK) 필드의 값을 DayOfWeek 열거체를 이용하여 반환|

\> Calendar 클래스에서는 1월을 0으로 표현하여 월의 범위가 0-11이었으며, 요일은 일요일부터 1로 표현<br>

\> TIME 패키지에서는 1월을 1로 표현하여 월의 범위가 1-12가 되었으며, 요일은 월요일부터 1로 표현

\### LocalDate - setter

|Method|Desc|

\|------|----|

|LocalDate with(TemporalField field, long newValue)|해당 날짜 객체에서 특정 필드를 전달된 새로운 값으로 설정한 새로운 날짜 객체를 반환|

|LocalDate withYear(int year)|해당 날짜 객체에서 연도(YEAR) 필드를 전달된 새로운 값으로 설정한 새로운 날짜 객체를 반환|

|LocalDate withMonth(int month)|해당 날짜 객체에서 월(MONTH\_OF\_YEAR) 필드를 전달된 새로운 값으로 설정한 새로운 날짜 객체를 반환|

|LocalDate withDayOfMonth(int dayOfMonth)|해당 날짜 객체에서 일(DAY\_OF\_MONTH) 필드를 전달된 새로운 값으로 설정한 새로운 날짜 객체를 반환|

|LocalDate withDayOfYear(int dayOfYear)|해당 날짜 객체에서 DAY\_OF\_YEAR 필드를 전달된 새로운 값으로 설정한 새로운 날짜 객체를 반환|

\### LocalTime - getter

|Method|Desc|

\|------|----|

|int get(TemporalField field)<br>long getLong(TemporalField field)|해당 시간 객체의 명시된 필드의 값을 int형이나 long형으로 반환|

|int getHour()|해당 시간 객체의 시(HOUR\_OF\_DAY) 필드의 값을 반환|

|int getMinute()|해당 시간 객체의 분(MINUTE\_OF\_HOUR) 필드의 값을 반환|

|int getSecond()|해당 시간 객체의 초(SECOND\_OF\_MINUTE) 필드의 값을 반환|

|int getNano()|해당 시간 객체의 나노초(NANO\_OF\_SECOND) 필드의 값을 반환|

\### LocalTime - setter

|Method|Desc|

\|------|----|

|LocalTime with(TemporalField field, long newValue)|해당 시간 객체에서 특정 필드를 전달된 새로운 값으로 설정한 새로운 시간 객체를 반환|

|LocalTime withHour(int hour)|해당 시간 객체에서 시(HOUR\_OF\_DAY) 필드를 전달된 새로운 값으로 설정한 새로운 시간 객체를 반환|

|LocalTime withMinute(int minute)|해당 시간 객체에서 분(MINUTE\_OF\_HOUR) 필드를 전달된 새로운 값으로 설정한 새로운 시간 객체를 반환|

|LocalTime withSecond(int second)|해당 시간 객체에서 초(SECOND\_OF\_MINUTE) 필드를 전달된 새로운 값으로 설정한 새로운 시간 객체를 반환|

|LocalTime withNano(int nanoOfSecond)|해당 시간 객체에서 나노초(NANO\_OF\_SECOND) 필드를 전달된 새로운 값으로 설정한 새로운 시간 객체를 반환|

\### 날짜, 시간 비교

|Method|Desc|

\|------|----|

|compareTo()|두 개의 날짜와 시간 객체를 비교|

|isEqual()|LocalDate 클래스에서만 제공되며, 날짜만을 비교|

|isBefore()|두 개의 날짜와 시간 객체를 비교하여 현재 객체가 명시된 객체보다 앞선 시간인지를 비교|

|isAfter()|두 개의 날짜와 시간 객체를 비교하여 현재 객체가 명시된 객체보다 늦은 시간인지를 비교|

📌 참고<br>

<http://tcpschool.com/java/java\_time\_localDateTime>{: target="\_blank"}<br>
