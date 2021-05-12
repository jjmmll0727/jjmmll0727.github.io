---
title: "recommendation of circles"
excerpt: "recommendation service that proceeded in double slash"
categories: "project"
---

<div style = "font-size: 20px; line-height: 25px;">
<center>recommendation college circle</center><br><br>
</div>

<P style = "font-style: 15px; line-heigt: 25px; text-align: left">
double slash에서 미니 프로젝트를 진행하고 나서 시작한 final project. <br>
경험 많은 개발자와 함께 프로젝트를 진행하면서 많은 것들을 배웠다. 
</p>

<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>1. branch & pr</strong><br>
</div>

<div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
미니 프로젝트를 진행할 때는 따로 브랜치를 따지 않고 master 브랜치에 지속적으로 작업을 했었다.
<br>
협업을 해야하는 프로젝트라면 반드시 브랜치를 따야 하지만, 내가 속해 있던 팀에서는 다들 협업이 처음이라 branch의 필요성을 알지 못했었다. <br>
하지만 팀을 재구성하여 파이널 프로젝트를 진행할 때는 팀장의 주도하에 fork 후, branch를 만들어 PR하는 방식으로 통일했었다. 
<br>
협업의 기본 자세를 배운 경험이었다. 
</p><br>
</div>
<p style = "font-size: 10px;"><a href = "https://github.com/Double-Slash/5th-final-team2.5/pull/10#event-4154276203">실제 feedback</a></p>
<div>
<center><img src = "\assets\images\fork.png" border=0></center> 
<center><img src = "\assets\images\branch.png" border=0></center>
</div>
<br>
<div style = "font-size: 15px; text-align: left; line-heignt:3em;"> PR feedback을 받으면서 알게 된 점 
<ul>
<li>loweCamelCase</li>
<li>PR 올릴때 불필요한 주석은 제외</li>
<li>validation check</li>
<li>let 보다 const 권장</li>
<li>== 보다 === 권장</li>
</ul>
</div>
<br>
<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>2. 비동기처리</strong><br>
</div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
미니 프로젝트에서 비동기처리를 하지 않은 것은 아니다. <br>
하지만, 파이널 프로젝트를 진행하면서 clean code를 배우면서 확실하게 알았다. 
많은 비동기 처리 방식이 있지만, 나는 이번 프로젝트를 통해서 callback의 단점과 promise의 단점을 보완한 async&await 방식을 사용했다. 
</p>

<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>3. prettier & eslint</strong><br>
</div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
처음 접해본 기술이다. <br>
code formatter prettier와 에러를 잡아주는 eslint<br>
협업을 하는데 있어서 반드시 필요한 tool(?) 이라고 생각한다. <br>
적용하는 방법은 간단하나, 이런 tool을 모른다면 정말 많은 불편함이 있을 것 같다는 생각이 든다.<br>
</p>
<p style = "font-size: 15px"><center>pritterrc.json</center></p>

```yaml
{
  "semi": true,
  "printWidth": 120,
  "tabWidth": 2,
  "trailingComma": "es5",
  "singleQuote": true,
  "jsxBracketSameLine": true,
  "arrowParens": "always",
}
```

<p style = "font-size: 15px"><center>eslintrc.json</center></p>

```yaml
{
  "env": { "browser": true, "es6": true, "node": true },
  "parser": "babel-eslint",
  "extends": ["eslint:recommended", "plugin:prettier/recommended"],
  "parserOptions":
    {
      "ecmaFeatures": { "jsx": true },
      "ecmaVersion": 2018,
      "sourceType": "module",
    },
  "plugins": ["prettier"],
}
```

<br>
<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>4. code style</strong><br>
</div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
express는 많은 개발자들이 사용하는 프레임워크로 다양한 코딩스타일이 존재한다. <br>
구글링을 통해서 봐도 전세계 사람들이 다양한 스타일로 restful api를 작성한다. <br>
하지만 이번에 파이널 프로젝트를 경험하면서 정말 깔끔하고 가독성이 좋은 스타일(module.exports로 한번에 모든 메소드 처리)을 배우게 되었다. 
</p>

```javascript
const signup = async (req, res) => {
  try {
    const { email, password, name, birth, phoneNumber } = req.body;
    if (!email || !password || !name || !birth || !phoneNumber) {
      return res
        .status(statusCode.BAD_REQUEST)
        .send(util.fail(statusCode.BAD_REQUEST, responseMessage.NULL_VALUE));
    }

    const salt = await bcrypt.genSalt(10);
    const hashedpw = await bcrypt.hash(password, salt);
    const user = await User.create({
      email,
      password: hashedpw,
      name,
      birth,
      phoneNumber,
    });
    return res
      .status(statusCode.CREATED)
      .send(
        util.success(statusCode.CREATED, responseMessage.SIGN_UP_SUCCESS, user)
      );
  } catch (err) {
    console.log(err);
    return res
      .status(statusCode.INTERNAL_SERVER_ERROR)
      .send(
        util.fail(
          statusCode.INTERNAL_SERVER_ERROR,
          responseMessage.SIGN_UP_FAIL
        )
      );
  }
};

// 로그인
const login = async (req, res) => {
  try {
    const { email, password } = req.body;
    if (!email || !password) {
      console.log("필요 입력 누락");
      return res
        .status(statusCode.BAD_REQUEST)
        .send(util.fail(statusCode.BAD_REQUEST, responseMessage.NULL_VALUE));
    }
    const checkEmail = await User.findOne({
      email,
    }).lean();
    if (!checkEmail) {
      console.log("없는 이메일");
      return res
        .status(statusCode.BAD_REQUEST)
        .send(util.fail(statusCode.BAD_REQUEST, responseMessage.NO_USER));
    }
    const checkPw = await bcrypt.compare(password, checkEmail.password);
    if (!checkPw) {
      console.log("비밀번호 불일치");
      return res
        .status(statusCode.BAD_REQUEST)
        .send(util.fail(statusCode.BAD_REQUEST, responseMessage.MISS_MATCH_PW));
    }

    const { _id, name, birth, phonenumber } = checkEmail; // 로그인하려는 사용자의 정보 중 일부만 추출
    const token = await jwt.sign(checkEmail);
    return res.status(statusCode.OK).send(
      util.success(statusCode.OK, responseMessage.SIGN_IN_SUCCESS, {
        token,
        user: { id: _id, name, birth, phonenumber },
      })
    );
  } catch (err) {
    console.log(err);
    return res
      .status(statusCode.INTERNAL_SERVER_ERROR)
      .send(
        util.fail(
          statusCode.INTERNAL_SERVER_ERROR,
          responseMessage.SIGN_IN_FAIL
        )
      );
  }
};

module.exports = {
  signup,
  login,
};
```

<br>
<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>5. status code 분리</strong><br>
</div>

<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
client와 data를 주고 받을때 예외처리를 반드시 해줘야 하는데, 이때 statuscode 와 response message를 분리하여 모듈화 하는 법을 배웠다.<br>
코드가 깔끔해지고 관리하기 더 용이했다. <br>
비록 단어나 멘트가 전문적이진 못하지만, 이렇게 따로 정리를 하고 개발을 진행하는 것이 팀원들끼리 의사소통을 하는데 있어서 수월했다. 
</p>

<p style = "font-size: 15px"><center>statuscode</center></p>

```yaml
module.exports = {
  OK: 200,
  CREATED: 201,
  NO_CONTENT: 204,
  RESET_CONTENT: 205,
  NOT_MODIFIED: 304,
  BAD_REQUEST: 400,
  UNAUTHORIZED: 401,
  FORBIDDEN: 403,
  NOT_FOUND: 404,
  INTERNAL_SERVER_ERROR: 500,
  SERVICE_UNAVAILABLE: 503,
};
```

<p style = "font-size: 15px"><center>response message</center></p>

```yaml
module.exports = {
  NULL_VALUE: '필요한 값이 없습니다.',
  OUT_OF_VALUE: '파라미터 값이 잘못 되었습니다.',

  /* Member */
  MEMBER_CREATE_SUCCESS: '회원 생성 성공',
  MEMBER_READ_SUCCESS: '회원 조회 성공',
  MEMBER_READ_ALL_SUCCESS: '전체 회원 조회성공',
  MEMBER_UPDATE_SUCCESS: '회원 수정 성공',
  MEMBER_DELETE_SUCCESS: '회원 삭제 성공',

  /* 회원가입 */
  SIGN_UP_SUCCESS: '회원가입성공',
  SIGN_UP_FAIL: '회원 가입 실패',
  SIGN_IN_SUCCESS: '로그인 성공',
  SIGN_IN_FAIL: '로그인 실패',
  ALREADY_ID: '존재하는 ID 입니다.',
  NO_USER: '존재하지않는 유저 id 입니다.',
  MISS_MATCH_PW: '비밀번호가일치하지않습니다',
  WRONG_NUMBER: '잘못된 휴대전화 번호입니다.', // 추가함..

  /* User */
  READ_USER_SUCCESS: '사용자 조회 성공',
  READ_USER_ALL_SUCCESS: '전체 사용자 조회 실패',
  READ_USER_FAIL: '사용자 조회 실패',
  READ_USER_ALL_FAIL: '전체 사용자 조회 실패',
  UPDATE_USER_SUCCESS: '사용자 업데이트 성공',
  UPDATE_USER_FAIL: '사용자 업데이트 실패',
  DELETE_USER_SUCCESS: '사용자 삭제 성공',
  DELETE_USER_FAIL: '사용자 삭제 실패',

  /* Post */
  CREATE_POST_SUCCESS: '게시글 생성 완료',
  CREATE_POST_FAIL: '게시글 생성 실패',
  READ_POST_FAIL: '게시글 조회 성공',
  READ_POST_ALL_FAIL: '전체 게시글 조회 실패',
  READ_POST_SUCCESS: '게시글 조회 실패',
  READ_POST_ALL_SUCCESS: '전체 게시글 조회 성공',
  UPDATE_POST_SUCCESS: '게시글 업데이트 성공',
  UPDATE_POST_FAIL: '게시글 업데이트 실패',
  DELETE_POST_SUCCESS: '게시글 삭제 성공',
  DELETE_POST_FAIL: '게시글 삭제 실패',

  /** Like */
  CREATE_LIKE_SUCCESS: '게시글 좋아요 성공',
  CREATE_LIKE_FAIL: '게시글 좋아요 실패',
  DELETE_LIKE_SUCCESS: '게시글 좋아요 취소하기 성공',
  DELETE_LIKE_FAIL: '게시글 좋아요 취소하기 실패',
  ALREADY_LIKED: '이미 좋아요가 되어 있음',

  /* 서버에러 */
  INTERNAL_SERVER_ERROR: '서버 내부 오류',
  EMPTY_TOKEN: '토큰 없음',
  EXPIRED_TOKEN: '만료된 토큰'
};
```
