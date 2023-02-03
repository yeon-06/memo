## 커밋 메시지 구조

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```
  
***

### type

- feat (feature)
- fix (bug fix)
- docs (documentation)
- style (formatting, missing semi colons, ...)
- refactor
- test (when adding missing tests)
- chore (maintain)
 
<br/>

### scope

- 커밋 변경 위치를 지정하는 것  
  ex: $location, $browser, $compile, $rootScope, ngHref, ngHref, ngClick, ...
 
<br/>

### subject

- 변경 사항에 대한 간결한 설명
- 현재 시제의 명령어 사용  
  (ex: changed X, changes X, change O)
- 첫 글자 대문자 금지
- 끝에 (.) 금지
 
<br/>

### body

- 변화에 대한 동기 및 이전과 비교
- 현재 시제의 명령어 사용

<br/>

### footer

- [breaking change](https://stackoverflow.com/questions/21703216/what-is-a-breaking-change-in-software) 기입  
  breaking change에 대한 설명, 정당성, 마이그레이션 참고글
 
<br/>

### 예제

```
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```

```
style($location): add couple of missing semi colons
```

```
docs(guide): updated fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```

***
참고: [https://gist.github.com/stephenparish/9941e89d80e2bc58a153﻿](https://gist.github.com/stephenparish/9941e89d80e2bc58a153﻿)
