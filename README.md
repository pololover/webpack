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




scripts부분이 길어지면서 webpack 고유의 파일이 필요하게 됨. -> webpack.config.js파일을 생성.


var path = require('path');  //ES5문법 common.js의 path라이브러리를 불러옴.


module.exports = {
  mode: 'none',
  entry:'./src/index.js',
  output : {
    filename : 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
}



npm run build 시 webpack.config.js파일 참조 -> index.js로 진입 후 dist디렉토리의 main.js에 통합.(main.js파일 내부에는 index.js의 내용과 사용한 라이브러리들의 내용이 담겨있음.) 



웹팩의 장점 : main.js에 모든 게 담겨있기 때문에 여러 URL에 요청을 보내지 않아도 됨. 즉 main.js에서 묶여져서 하나의 파일안에서 처리하기 때문에 부하가 적고 속도도 빠름.
