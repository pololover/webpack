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

웹팩에서의 모듈은 웹 애플리케이션을 구성하는 모든 자원을 의미한다.

웹팩의 등장배경
1) 파일 단위로 변수를 관리하기 위해. 
2) 웹 개발 작업 자동화 도구 -> 새로고침 및, 웹 개발에 쓰이는 자원들을 압축하는 것을 자동화하기위해
3) 웹의 빠른 로딩속도와 높은 성능

웹팩의 철학 : 기본적으로 필요한 자원은 미리 로딩하는 게 아니라 그때그때 요청하자는 철학

브라우저별 HTTP의 제약이 있는데 이를 해결하는 것도 웹팩.

웹팩은 Dynamic Loading과 Lazy Loading도 지원을 해준다.

babel은 자바스크립트가 여러 브라우저들과 호환가능한 형태로 바꿔주는 컴파일러이다.

dependescies에 있는 것들에 대해서 npm i를 해주면 전부 node_modules폴더에 들어가게 된다.

웹팩의 기능중에는 source map이라는 기능이 있는데 이를 devtool : 'sourcemap'으로 설정해주면 컴파일된 코드를 원래코드로 매핑해주게 된다. 이는 트래킹을 위해사용되며 여러 js파일들이 하나의 번들파일로 합쳐졌을때 에러를 보다 빠르고 직관적이게 찾을 수 있게된다.

webpack.config.js파일에서 entry(진입점)은 2개 이상이 될 수도 있다. 따라서 bundle파일이 진입점 수에맞게 생성된다.  

webpack.config.js파일의 output부분에서 파일이름에 이름값과 청크해쉬값 두개를 넣어주는게 일반적이다. ex) [name].[chunkhash].bundle.js

css loader의 역할 : js파일에서 css파일을 import했을때 웹팩의 css loader는 이를 알아서 적용시켜준다.

loader를 이용하기위해선 module 밑에 rules가 필요하다. rules밑에 여러개의 loader에대한 규칙을 설정해주는데 test는 적용할 파일들, use에는 사용할 loader 커멘드를 입력해주면 된다.

css loader의 역할은 css코드를 웹팩안에 넣어주는 것이고 style loader의 역할은 웹팩안의 css코드를 head의 style에 위치시키는 것이다. 

loader가 여러개 있을때 순서도 중요하다. loader판별은 오른쪽에서 왼쪽으로 인식하기 때문에 개발자의 의도에 맞춰 정의하는 것이 중요하다.

플러그인은 객체로 저장.

웹팩의 플러그인은 결과물을 변화시킨다는 점을 기억.

플러그인은 웹팩의 기본적인 동작에 추가적인 기능을 제공한다. 

플러그인을 로더와 비교하자면 로더는 파일을 해석하고 변환하는 과정에 관여하고 플러그인은 해당 결과물의 형태를 바꿔준다.

플러그인의 배열에는 생성자 함수로 생성한 객체 인스턴스만 추가될 수 있다.

javascript파일이 아닌 css파일 html과같은 파일들은 로더를 통해 변환(번들링)이 되어야한다.

code-spliting은 웹 팩의 가장 강력한 기능 중 하나이다. 이는 코드를 다양한 번들로 분할한 뒤 요청 시 병렬로 로드할 수 있으며 리소스 로드 우선순위를 제어할 수 있다. 이를 올바르게 사용한다면 로드 시간에 큰 영향을 줄 것이다.

웹팩은 엔트리 파일 하나만 설정한다면 import하거나 사용하고 있는 라이브러리들을 자동적으로 해석준다.

webpack dev server : 웹팩의 빌드 대상 파일이 변경되었을때 매번 웹팩 명령어를 실행하지 않아도 코드만 변경하고 저장하면 웹팩으로 빌드한 후 브라우저를 새로고침 해줌.

웹팩 데브서버는 빌드한 결과물이 파일 탐색기나 프로젝트 폴더에서 보이지 않는데 이는 결과물이 파일로 생성되지않고 메모리에 저장되기 때문이다. 따라서 
컴퓨터 구조 관점에서 파일 입출력보다 메모리 입출력이 더 빠르고 컴퓨터 자원이 덜 소모가 된다.

npm run dev는 웹팩 데브서버를 이용할 수 있다.

HtmlWebpackPlugin은 웹팩 빌드 결과물에 대해서 html 템플릿을 만들어주고 그 안에 빌드 내용들까지 포함해준다. 또한 이는 css파일과 js파일을 각각 html파일에 link태그와 script
태그로 추가하는 것을 자동으로 해준다.

webpack의 production모드와 development의 차이는 전자는 배포용이기에 번들의 최소화 및 가벼운 소스맵 및 애셋 최적화를 초점으로 변경이 되는 것이고, 후자는 라이브 리로딩 및 hot
module replacement 기능을 원하기에 둘은 지향하고자 하는 바가 다르다.

devserver에 overlay는 빌드시 에러나 경고를 브라우져 화면에 표시해줌.

진입점이 한개든 두개든 main.js 또는 bundle.js 하나의 파일로 번들링 해주기때문에 request가 늘거나 하지 않는다.

webpack의 resolve 속성은 파일을 해석할때 편의성을 더한 기능이다. alias는 별칭, extensions은 뒤에 확장자를 붙이지않아도 해석할 수 있도록 하는 것.

