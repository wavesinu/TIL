### LoginService 구현
```java
@Service
@RequiredArgsConstructor
public class LoginService {

    private final MemberRepository memberRepository;
    
    public Member login(String loginId, String password) {
        return memberRepository.findByLoginId(loginId)
        .filter(m -> m.getPassword().equals(password))
        .orElse(null);
    }
}
```
회원을 조회한 다음, 파라미터로 넘어온 password와 비교해서 같을 경우 회원을 반환하고, password가 다르면 `null`을 반환한다.
### LoginController 구현
```java
@Slf4j
@Controller
@RequiredArgsConstructor
public class LoginController {

    private final LoginService loginService;

    @GetMapping("/login")
    public String loginForm(@ModelAttribute("loginForm") LoginForm loginForm) {
        return "login/loginForm";
    }

    //실제 로그인이 처리되는 로직
    @PostMapping("/login")
    public String login(@Valid @ModelAttribute LoginForm form, BindingResult bindingResult) {

        if (bindingResult.hasErrors()) {
            return "login/loginForm";
        }

        Member loginMember = loginService.login(form.getLoginId(), form.getPassword());
        if (loginMember == null) {
            //특정 필드에 대한 오류가 아님
            bindingResult.reject("loginFail", "아이디 또는 비밀번호가 맞지 않습니다.");
            return "login/loginForm";
        }

        //로그인 성공 처리 TODO

        //home으로 redirect
        return "redirect:/";
    }
}
```
---
# 로그인 처리 - 쿠키 사용
### 로그인 상태 유지하기
쿼리 파라미터를 계속 유지하면서 보내는 것은 어려운 작업이므로 쿠키([[Cookie]])를 사용한다.
서버에서 로그인에 성공하면 HTTP 응답에 쿠키를 담아 브라우저에 전달한다. 그러면 브라우저는 앞으로 해당 쿠키를 지속해서 보내준다.
