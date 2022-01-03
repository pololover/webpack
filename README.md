# webpack

모듈 번들링 : 파일들을 전부 해석한 뒤에 그 파일들을 하나로 합쳐주는 것.

webpack은 모듈 번들러.

npm init -y -> package.json 생성

package.json에서 scripts부분은 임의로 정의할 수 있는 부분.

"scripts": {
    "build" : "webpack --mode=none" 
 }

npm run build시 webpack --mode-none이 실행된다. 

mode를 설정함으로써 warning이 나오지 않고, 코드가 복잡하게 압축되지 않는다.



