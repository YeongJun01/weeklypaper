### 🇶 Express.js에서 미들웨어란 무엇인지 설명해 주세요.

- 미들웨어란 크라이언트에게 요청이 오고 그 요청을 보내기 위해 응답하려는 중간(미들)에 목적에 맞게 처리를 하는 함수들이라고 보면 된다.
- 미들웨어 함수는 req(요청)객체, res()객체 그리고 어플리케이션 요청-응답 사이클 도중 그 다음의 미들웨어 함수에 대한 엑세스 권한을 갖는 함수이다.
- 다음 미들웨어 함수에 대한 엑세스는 next함수를 이용해서 다음 미들웨어로 현재 요청을 넘길 수 있다.
- next를 통해 미들웨어는 순차적으로 처리된다.

```javascript
export function defaultNotFoundHandler(req, res, next) {
  return res.status(404).send({ message: "Not found" });
}
```

- 진행했던 프로젝트의 에러 핸들러 일부를 가져왔다. 위처럼 미들웨어는 req, res, next를 인자로 받는다.

### 🇶 백엔드 서버에서 이미지 업로드를 구현하는 다양한 방식에 대해 설명해 주세요.

- 다양한 방식이라기 보단 multer를 많이 사용했왔다.
- multersms 이미지, 동영상 PDF 같은 파일을 포함하는 HTTP 요청을 읽을 수 있게 해준다. 일반적인 JSON 요청은 body-parser가 처리할 수 있지만 파일이 포함된 요청은 multer가 필요하다.
  <br/>
  |기능|설명|
  |:---:|:---:|
  |파일 업로드 처리|클라이언트가 보낸 파일을 서버에서 받아서 저장|
  |메모리 또는 디스크 저장|파일을 메모리에 버퍼로 저장하거나 서버 디스크에 직접 저장 가능|
  |다양한 옵션|파일 크기 제한, 확장자 제한, 업로드 경로 지정 가능|
  |단일/다중 파일 업로드 지원|.single(), .array(), .fields() 등 다양한 업로드 형태 지원|
  <br/>
- 예시

```javascript
import multer from "multer";

const upload = multer({ dest: "uploads/" });

app.post("/upload", upload.single("image"), (req, res) => {
  console.log(req.file);
  res.send("업로드 완료");
});
```
