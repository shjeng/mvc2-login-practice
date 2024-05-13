<h2>로그인 처리2 - 필터, 인터셉터</h2>

<h3>서블릿 필터-인증 체크</h3>

<h5>정상 흐름</h5>
* 'preHandle': 컨트롤러 호출 전에 호출된다.(더 정확히는 핸들러 어댑터 호출 전에 호출)
  * 'preHandle'의 응답값이 'true'이면 다음으로 진행, 'false'면 더는 진행하지 않음. 'false'인 경우 나머지 인터셉터는 물론이고, 핸들러 어댑터도 호출되지 않음.
* 'postHandle': 컨트롤러 호출 후에 호출된다.(더 정확히는 핸들러 어댑터 호출 후에 호출된다.)
* 'afterCompletion': 뷰가 렌더링 된 이후에 호출된다.

<h5>예외가 발생시 </h5> 
* 'preHandle': 컨틀롤러 호출 전에 호출된다.
* 'postHandle': 컨트롤러에서 예외가 발생하면 'postHandle'은 호출되지 않는다.
* 'aftercompleteion': afterCompletion'은 항상 호출된다. 이 경우 예외('ex')를 파라미터로 받아서 어떤 예외가 발생했는지 로그로 출력할 수 있다.

<h5>afterCompletion은 예외가 발생해도 호출된다.</h5>
* 예외가 발생하면 'postHandle()'는 호출되지 않으므로 예외와 무관하게 공통 처리를 하려면 'afterCompletion()'을 사용해야 한다.
* 예외가 발생하면 'afterCompletion()'에 예외 정보('ex')를 포함해서 호출된다.

<h5>인터셉터는 스프링 MVC 구조에 특화된 필터 기능을 제공한다고 이해하면 된다. 스프링 MVC를 사용하고, 특별히 필터를 꼭 사용해야 하는 상황이 아니라면 인터셉터를 사용하는 것이 편리하다.</h5>

<hr>
<h3>서블릿 필터-요청로그</h3>
<h5>'HandlerMethod'</h5>
* 핸들러 정보는 어떤 핸들러 매핑을 사용하는가에 따라 달라진다. 스프링을 사용하면 일반적으로 '@Controller', '@RequestMapping'을 활용한 핸들러 매핑을 사용하는데, 이 경우 핸들러 정보로 ' HandlerMethod'가 넘어온다.
<h5>'ResourceHttpReuqestHandler'</h5>
* '@Controller'가 아니라 '/resources/static'와 같은 정적 리소스가 호출 되는 경우 'ResourceHttpRequestHandler'가 핸들러 정보로 넘어오기 때문에 타입에 따라서 처리가 필요하다. 

<h5>'postHandle, afterCompletion'</h5>
* 종료 로그를 'postHandle'이 아니라 'afterCompletion'에서 실행한 이유는, 예외가 발생한 경우 'postHandler'가 호출되지 않기 때문이다. 'afterCompletion'은 예외가 발생해도 호출 되는 것을 보장한다. 

<hr>