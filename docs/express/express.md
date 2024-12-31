---
layout: default
title: Express
nav_order: 11
has_children: true
---

# Express

## 기본적인 사용법

```javascript
const app = express();

app.get('/test',(req,res)=>())


app.listen(3000, () => console.log('서버가 시작되었습니다'));
```

위와 같이 세팅하면 app 변수로 라우트를 진행할수있다.

get 메소드의 인수는...

- 첫번째 인수는 url 경로
- 두번째 인수는 콜백 함수

모든 메소드는 사실 다음과 같은 형식을 따른다.

`app.method(path, handler)`

- method : 메소드 이름
- path : 엔드포인트 경로
- handler : 콜백함수 -> 이때 여기 인수 두개는 첫번째는 리퀘스트 두번쨰는 리스폰스 객체이다.

```javascript
app.get("/test", (req, res) => res.send(somethingData));
```

res.send 메소드는 자바스크립트 객체나 배열을 전달할경우 json 으로 컨버트 시켜준다 추가로 content-type도 설정해준다.

```javascript
app.get("/test", (req, res) => {
  const sort = req.query.sort;
  const count = Number(req.query.count);

  let newDatas = somethingData.sort((a, b) =>
    sort === "oldest" ? a.createdAt - b.createdAt : b.createdAt - a.createdAt
  );

  if (count) {
    newDatas = newDatas.slice(0, count);
  }
  res.send(newDatas);
});
```

쿼리 파라미터는 쿼리라는 객체에 저장이 된다. 모두 문자열로 넘어오기에 형변환이 필요하다

```javascript
app.get("/test/:id", (req, res) => {
  const id = Number(req.params.id);
  const data = somethingDatas.find((data) => data.id === id);
  if (data) {
    res.send(data);
  } else {
    res.status(404).send({ message: "Cannot find task" });
  }
});
```

위와같이 다아니믹 url로 원하는 아이디 데이터를 가져올수있다.

`res.status(404)`는 리스폰스의 상태코드를 설정한다.

```javascript
app.use(express.json());
```

리퀘스트 바디를 파싱해서 자바스크립트 객체로 바꾸려면 위와 같은 작업을 해주어야한다.

```javascript
app.post("/test", (req, res) => {
  const newData = req.body;
  const ids = somethingDatas.map((data) => data.id);
  newData.id = Math.max(...ids) + 1;
  newData.isComplete = false;
  newData.createdAt = new Date();
  newData.updatedAt = new Date();
  somethingDatas.push(newData);
  res.status(201).send(newData);
});
```

위와같이 기존데이터에 객체를 만들어서 추가해주면 새로운 데이터를 POST 할수있다.

```javascript
app.patch("/test/:id", (req, res) => {
  const id = Number(req.params.id);
  const data = somethingDatas.find((data) => data.id === id);
  if (data) {
    Object.keys(req.body).forEach((key) => {
      data[key] = req.body[key];
    });
    data.updatedAt = new Date();
    res.send(data);
  } else {
    res.status(404).send({ message: "Cannot find data" });
  }
});
```

데이터를 업데이트 하고싶다면 patch를 써서 업데이트 가능하다

```javascript
app.delete("/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const idx = tasks.findIndex((task) => task.id === id);
  if (idx >= 0) {
    tasks.splice(idx, 1);
    res.sendStatus(204);
  } else {
    res.status(404).send({ message: "Cannot find id" });
  }
});
```

delete로 지울수있다. 인덱스를 찾아 splice로 지웠다.

`res.sendStatus(204)`는 리스폰스로 바디없이 상태코드만 보낸다.

```javascript

```
