- **💁‍♀️ 6.08. setTimeout과 setInterval을 이용한 호출 스케줄링**
    
    <aside>
    💡
    
    - `setTimeout`을 이용해 일정 시간이 지난 후에 함수를 실행하는 방법
    - `setInterval`을 이용해 일정 시간 간격을 두고 함수를 실행하는 방법
    </aside>
    
    ### setTimeout
    
    : 일정 시간이 지난 후 함수 실행
    
    ```jsx
    **//함수에 인수 넘기기 가능!**
    
    function sayHi(who, phrase) {
      alert( who + ' 님, ' + phrase );
    }
    
    setTimeout(sayHi, 1000, "홍길동", "안녕하세요."); // 홍길동 님, 안녕하세요.
    ```
    
    - **clearTimeout으로 스케줄링 취소하기**
        
        ```jsx
        let timerId = setTimeout(...);
        clearTimeout(timerId);
        ```
        
        ```jsx
        let timerId = setTimeout(() => alert("아무런 일도 일어나지 않습니다."), 1000);
        alert(timerId); // 타이머 식별자
        
        clearTimeout(timerId);
        alert(timerId); // 위 타이머 식별자와 동일함 (취소 후에도 식별자의 값은 null이 되지 않습니다.)
        ```
        
    
    ### setInterval
    
    : 일정 간격을 두고 함수 실행
    
    ```jsx
    // 2초 간격으로 메시지를 보여줌
    let timerId = setInterval(() => alert('째깍'), 2000);
    
    // 5초 후에 정지
    setTimeout(() => { clearInterval(timerId); alert('정지'); }, 5000);
    ```
    
    **📛 alert 창이 떠 있더라도 타이머는 멈추지 않는다.**
          대부분의 브라우저는 alert/confirm/prompt 창이 떠 있는 동안에도 내부 타이머를 멈추지 않는다.
    
    ### 중첩 setTimeout
    
    : 무언가를 일정 간격을 두고 실행하는 방법 : 1. 중첩 setTimeout / 2. setInterval
    
    - 중첩 `setTimeout`은 지연 간격을 보장하지만 `setInterval`은 이를 보장하지 않는다.
        - `setInterval`  사용
            
            ```jsx
            //내부 스케줄러가 func(i++)를 100밀리초마다 실행
            
            let i = 1;
            setInterval(function () {
            	func(i++);
            }, 100);
            ```
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/b042c06e-3986-4db9-baf6-4b8d3b7a9ccf/image.png)
            
            ⇒ **`setInterval` 사용 시 func호출 사이의 지연 간격이 실제 명시한 간격(100ms)보다 짧아짐!!!**
            
            : 짧아지는 이유 → func을 실행하는 데 ‘소모되는’ 시간도 지연 간격에 포함되기 때문!
            
        - 중첩 `setTimeout`  사용
            
            ```jsx
            let i = 1;
            setTimeout(function run() {
            	func(i++);
            	setTimeout(run, 100);
            }, 100);
            ```
            
            ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/579af2d6-e324-415e-9852-1ab48e096ca7/image.png)
            
            ⇒ 중첩 **`setTimeout` 사용 시 명시한 지연(100ms)이 보장!!!!**
            
            : 보장되는 이유 → 이전 함수 실행 종료 후 다음 함수 호출에 대한 계획이 세워지기 때문!
            
        
    
    **📛 가비지 컬렉션과 setInterval, setTimeout
    ●** `setInterval`과 `setTimeout`에 넘긴 함수는 가비지 컬렉션의 대상이 되지 않는다.
    ⇒ 이유 : `setInterval`과 `setTimeout`에 넘긴 함수는 일정 시간 뒤 실행 및 반복을 위해 자바스크립   트의 ‘스케줄러’가 함수를 기억 → 기억을 위해 함수에 대한 내부 참조가 만들어지고, 스케줄러가 이 참조를 가지고 있기 때문에 메모리에서 제거되지 않는다.
    **●** 메모리 문제 발생 위험으로 필요 없는 `setTimeout`이나 `setInterval`을 잊지 말고 **취소**
    `setTimeout`은 `clearTimeout()`, `setInterval`은 `clearInterval()`로 취소할 수 있다. 이를 통해 함수에 대한 참조를 제거하고, 가비지 컬렉션이 제대로 동작하도록 도와 메모리 누수를 방지할 수 있다.
    
    ### 대기 시간이 0인 setTimeout
    
    `setTimeout(func, 0)` `setTimeout(func)` 사용 시 `setTimeout` 대기 시간 0으로 설정 가능
    
    현재 스크립트 실행 종료된 ‘직후’ 원하는 함수 실행 가능!
    
    ```jsx
    **//Hello 이후 바로 World 실행!!!**
    setTimeout(() => alert("World"));
    alert("Hello");
    ```
    
    ---
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/681aabec-185e-44d0-b64b-3d352bfbfae8/4145b774-409a-441c-87ae-4d43dd97a7db/image.png)
    
    ---
    
    ---