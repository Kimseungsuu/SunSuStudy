## ๐ค @PathVariable ์ด๋?
REST API์์ URI์ ๋ณ์๊ฐ ๋ค์ด๊ฐ๋๊ฑธ ์ค๋ฌด์์ ๋ง์ด ๋ณผ ์ ์๋ค.

์๋ฅผ ๋ค๋ฉด, ์๋ URI์์ ๋ฐ์ค ์น ๋ถ๋ถ์ด @PathVariable๋ก ์ฒ๋ฆฌํด์ค ์ ์๋ ๋ถ๋ถ์ด๋ค.

http://localhost:8080/api/user/1234

https://music.bugs.co.kr/album/4062464

## ์ฌ์ฉ๋ฒ
Controller์์ ์๋์ ๊ฐ์ด ์์ฑํ๋ฉด ๊ฐ๋จํ๊ฒ ์ฌ์ฉ ๊ฐ๋ฅํ๋ค.

@GetMapping(PostMapping, PutMapping ๋ฑ ๋ค ์๊ด์์)์ {๋ณ์๋ช}

๋ฉ์๋ ์ ์์์ ์์ ์ด ๋ณ์๋ช์ ๊ทธ๋๋ก @PathVariable("๋ณ์๋ช")

(Optional) Parameter๋ช์ ์๋ฌด๊ฑฐ๋ ์๊ด์์(์๋์์ String name๋ OK, String employName๋ OK)

    @RestController
    public class MemberController {
    // ๊ธฐ๋ณธ
    @GetMapping("/member/{name}")
    public String findByName(@PathVariable("name") String name ) {
    return "Name: " + name;
    }
    // ์ฌ๋ฌ ๊ฐ
    @GetMapping("/member/{id}/{name}")
	public String findByNameAndId(@PathVariable("id") String id, @PathVariable("name") String name) {
    	return "ID: " + id + ", name: " + name;
        }
    }

์ถ์ฒ: https://byul91oh.tistory.com/435