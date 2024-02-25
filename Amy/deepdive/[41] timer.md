##### | 모던 자바스크립트 DeepDive <br />

###### range: 41. 타이머 <br />

###### date: day28 (2024.02.25) <br />

<hr />
<br />

## 호출 스케줄링

함수를 명시적으로 호출하면 함수가 즉시 실행 <br />
만약 함수를 명시적으로 호출하지 않고 일정 시간이 경과된 이후에 호출되도록 함수 호출을 예약하려면 타이머 함수를 사용해야 하는데 이를 호출 스케줄링(scheduling a call)이라 한다.

<br />

JS에서 제공하는 타이머 함수 <br />

1️⃣ 타이머를 생성할 수 있는 타이머 함수 setTimeout / setInterval <br />
2️⃣ 타이머를 제거할 수 있는 타이머 함수 clearTimeout / clearInterval <br />

<br />

타이머 함수는 ECMAScript 사양에 정의된 빌트인 함수가 아니다. <br />
브라우저 환경과 Node.js 환경에서 모두 전역 객체의 메서드로서 타이머 함수를 제공한다. <br />
즉, 타이머 함수는 호스트 객체이다. <br />

setTimeout 함수가 생성한 타이머는 단 한 번 동작하고, setInterval 함수가 생성한 타이머는 반복 동작한다. <br />

자바스크립트 엔진은 단 하나의 실행 컨텍스트 스택을 갖기 때문에 두 가지 이상의 태스크(task)를 동시에 실행할 수 없다. <br />
즉, 자바스크립트 엔진은 싱글 스레드로 동작한다. 이러한 이유로 타이머 함수는 비동기 처리 방식으로 동작한다. <br />

<br />

### 타이머 함수

```javascript
const timeoutdId = setTimeout(func|code[, delay, param1, param2, ...]);
```

<table>
    <tr>
        <td>매개변수</td>
        <td>설명</td>
    </tr>
    <tr>
        <td>func</td>
        <td>타이머가 만료된 뒤 호출될 콜백 함수.<br />콜백 함수 대신 코드를 문자열로 전달 가능.<br />이때 코드 문자열은 타이머가 만료된 뒤 해석되고 실행.</td>
    </tr>
    <tr>
        <td>delay</td>
        <td>타이머 만료 시간(밀리초(ms) 단위), setTimeout 함수는 delay 시간으로 단 한 번 동작하는 타이머를 생성.<br />인수 전달을 생략한 경우 기본 값 0이 지정.</td>
    </tr>
    <tr>
        <td>param1, param2, ...</td>
        <td>호출 스케줄링된 콜백 함수에 전달해야 할 인수가 존재하는 경우 세 번째 이후의 인수로 전달 가능.</td>
    </tr>
</table>

<br />

setTimeout 함수는 생성된 타이머를 식별할 수 있는 고유한 타이머를 식별할 수 있는 고유한 id를 반환한다. setTimeout 함수가 반환한 타이머 id는 아래와 같다 :

1️⃣ 브라우저 환경일 경우 숫자 <br />
2️⃣ Node.js 환경인 경우 객체 <br />

setTimeout 함수가 반환한 타이머 id를 clearTimeout 함수의 인수로 전달하여 타이머를 취소할 수 있다.

<br />

### setInterval/ clearInterval

setInterval 함수는 두 번째 인수로 전달받은 시간(ms, 1/1000초)으로 반복 동작하는 타이머를 생성한다.

setInterval의 첫 번째 인수인 콜백 함수는 두 번째 인수로 전달받은 시간이 경과할 때마다 반복 실행되도록 호출 스케줄링된다.

setInterval 함수는 생성된 타이머를 식별할 수 있는 고유한 타이머 id를 반환한다. Node.js 환경인 경우 객체를 반환한다.

<br />

### 디바운스와 스로틀

scroll, resize, mousemove 같은 이벤트는 짧은 시간 간격으로 연속해서 발생한다. 이러한 이벤트에 바인딩한 이벤트 핸들러는 과도하게 호출되어 성능에 문제를 일으킬 수 있다.

디바운스와 스로틀은 **짧은 시간 간격으로 연속해서 발생하는 이벤트를 그룹화**해서 **과도한 이벤트 핸들러의 호출을 방지**하는 프로그래밍 기법이다.

```javascript
<!DOCTYPE html>
<html>
  <body>
    <button>click me</button>
    <pre>일반 클릭 이벤트 카운터    <span class="normal-msg">0</span></pre>
    <pre>디바운스 클릭 이벤트 카운터 <span class="debounce-msg">0</span></pre>
    <pre>스로틀 클릭 이벤트 카운터   <span class="throttle-msg">0</span></pre>
    <script>
      const $button = document.querySelector("button");
      const $normalMsg = document.querySelector(".normal-msg");
      const $debounceMsg = document.querySelector(".debounce-msg");
      const $throttleMsg = document.querySelector(".throttle-msg");

      const debounce = (callback, delay) => {
        let timerId;
        return (event) => {
          if (timerId) clearTimeout(timerId);
          timerId = setTimeout(callback, delay, event);
        };
      };

      const throttle = (callback, delay) => {
        let timerId;
        return (event) => {
          if (timerId) return;
          timerId = setTimeout(
            () => {
              callback(event);
              timerId = null;
            },
            delay,
            event
          );
        };
      };

      $button.addEventListener("click", () => {
        $normalMsg.textContent = +$normalMsg.textContent + 1;
      });

      $button.addEventListener(
        "click",
        debounce(() => {
          $debounceMsg.textContent = +$debounceMsg.textContent + 1;
        }, 500)
      );

      $button.addEventListener(
        "click",
        throttle(() => {
          $throttleMsg.textContent = +$throttleMsg.textContent + 1;
        }, 500)
      );
    </script>
  </body>
</html>
```

#### debounce

디바운스(debounce)는 짧은 시간 간격으로 이벤트가 연속해서 발생하면 이벤트 핸들러를 호출(call)하지 않다가 일정 시간이 경과된 이후에 이벤트 핸들러가 한 번만 호출되도록 한다.

즉 디바운스는 짧은 시간 간격으로 발생하는 이벤트를 그룹화해서 마지막에 한 번만 이벤트 핸들러가 호출되도록 한다.

<br />

#### throttle

쓰로틀(throttle)은 짧은 시간 간격으로 이벤트가 연속해서 발생하더라도 일정 시간 간격으로 이벤트 핸들러가 최대 한 번만 호출되도록 한다.

스로틀은 짧은 시간 간격으로 연속해서 발생하는 이벤트를 그룹화해서 일정 시간 단위로 이벤트 핸들러가 호출되도록 호출 주기를 만든다.

<br />
