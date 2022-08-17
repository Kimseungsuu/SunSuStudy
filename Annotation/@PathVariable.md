## 🤔 @PathVariable 이란?
REST API에서 URI에 변수가 들어가는걸 실무에서 많이 볼 수 있다.

예를 들면, 아래 URI에서 밑줄 친 부분이 @PathVariable로 처리해줄 수 있는 부분이다.
http://localhost:8080/api/user/1234
https://music.bugs.co.kr/album/4062464

## 사용법
Controller에서 아래와 같이 작성하면 간단하게 사용 가능하다.

@GetMapping(PostMapping, PutMapping 등 다 상관없음)에 {변수명}

메소드 정의에서 위에 쓴 변수명을 그대로 @PathVariable("변수명")

(Optional) Parameter명은 아무거나 상관없음(아래에서 String name도 OK, String employName도 OK)

    @RestController
    public class MemberController {
    // 기본
    @GetMapping("/member/{name}")
    public String findByName(@PathVariable("name") String name ) {
    return "Name: " + name;
    }
    // 여러 개
    @GetMapping("/member/{id}/{name}")
	public String findByNameAndId(@PathVariable("id") String id, @PathVariable("name") String name) {
    	return "ID: " + id + ", name: " + name;
        }
    }

출처: https://byul91oh.tistory.com/435