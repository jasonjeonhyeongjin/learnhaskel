

## 모나드 괴담

엑스티
2015년 11월 14일

---

## 온갖 음해에 시달렸습니다

- 하스켈은 어렵다
- 모나드가 어려워서 하스켈은 어렵다
- 모나드를 알아야 하스켈을 쓸 수 있다
    - 모나드를 알아야 _실용적_ 하스켈을 쓸 수 있다
- 하스켈은 수학적인 언어다
- 아무튼 모나드를 배워야 한다

--

**NO**

---

## 저 혼자만의 생각이 아닙니다.

- Dan Piponi, _[The IO Monad for People who Simply Don't Care](http://blog.sigfpe.com/2007/11/io-monad-for-people-who-simply-dont.html)_ (2007)
- Brent Yorgey, _[Abstraction, intuition, and the “monad tutorial fallacy”](https://byorgey.wordpress.com/2009/01/12/abstraction-intuition-and-the-monad-tutorial-fallacy/)_ (2009)
- tora, _[My how to give a 'monad tutorial' tutorial](http://www.doc.ic.ac.uk/~tora/monadsI.txt)_ (2010)
- scottw, _[Why I won't be writing a monad tutorial](http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/)_ (2013)
- Travis Hance, _[Write you a monad tutorial](https://tjhance.quora.com/Write-you-a-monad-tutorial)_ (2014)
- ~kqr, _[The "What Are Monads?" Fallacy](http://two-wrongs.com/the-what-are-monads-fallacy)_ (2015)
- Justin Le, _[IO Monad Considered Harmful](http://blog.jle.im/entry/io-monad-considered-harmful)_ (2015)

"왜 무수한 하스켈 초보자들이 똑같은 (잘못된) 질문을 하고, 똑같은 (겪지 않아도 될) 어려움을 겪는 것일까?"에 대한 문제의식이 최근 몇 년간 형성되기 시작함

---

## 1년 가까이 하스켈 모임을 운영해보니...

독보적으로 많이 들은 이야기 1위

---

class: center, middle

## 모나드가 뭐죠?

--
...는 아니고요

---

class: center, middle

## 하스켈이 그렇게 좋은 언어라면 왜 많이들 안 쓰나요?

---

class: center, middle

![facepalm](/static/img/haskell/monad_fear/facepalm.jpg)

([Photo](http://www.flickr.com/photos/proimos/4199675334/) by [Alex E. Proimos](http://www.flickr.com/photos/proimos/). Released under the [Creative Commons Attribution 2.0 Generic](https://creativecommons.org/licenses/by/2.0/deed.en) license.)

---

## 물론 하스켈만의 이유가 있기는 합니다.

- "Avoid success at all cost": 성공하면 하위호환성을 깰 수 없다. 성공하지 말고 계속 혁신하자
- 하스켈에서 성공적으로 검증된 개념이 다른 언어에 받아들여지는 사례 증가
    - 파이선의 List comprehension
    - 러스트의 Trait, C++의 Concept, 자바의 저네릭스
    - Maybe chain
    - ...
- 스스로 성공하지 않되 다른 모든 프로그래밍 언어의 발전을 선도하는 언어
- 그럼에도, 최근 상업적으로 상당한 쓰임을 보이고 있음
- 아무튼, 오늘 하려는 얘기는...

---

class: center, middle

## 모나드를 이해해 보려고 했는데 너무 어렵더라고요.

---

class: center, middle

## 하스켈 너무 어려워요. 무슨 말인지 하나도 모르겠어요.

---

## 광범위한 교수법적 실패

- "하스켈이란 무엇인가?"로 찾아보면
    - 순함수형(purely functional) 프로그래밍 언어다.
    - 게으른(lazy) 언어다.
    - 모나드(monad)를 쓴다.
    - 타입클래스(typeclass).
    - 기타 등등.
--
- 대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들

--
- **모르는 것을 설명하기 위해서 모르는 개념을 동원한다**

--
- ?!

--
- 어렵다고 난리가 날 수밖에...
--
 ㅠㅠ

---

class: center, middle

## 하스켈이라는 언어는 왜 만들어졌는가?

---

## Haskell 2010 Report

### Preface

[...]

#### Goals

> 1. It should be suitable for teaching, research, and **applications, including building large systems**.

--

- 언어 설계의 목표 가운데 애플리케이션 개발용으로 적합하여야 한다는 요건이 명기되어 있다.

---

## 하스켈 위원회가 조직된 배경

--
- 1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다

--
- 선택지가 너무 많아서 노력이 분산되고, 시장에서는 하나도 선택받지 못하는 상황

--
- 순함수형이 좋은 생각 같은데 더 널리 쓰이지 못하니 안타깝다. 그러니 하나로 뭉쳐 **선택받는 언어를 만들어보자.**

--
- 즉, **학술 연구 전용 언어가 아니다.**

--
- **현실에서 쓰이겠다는 목표를 가지고 만들어졌다**.

---

## 하스켈은 현실의 문제를 해결하는 현실의 도구입니다

- C보다 고성능인 웹 서버
- 스탠다드 차타드: "real time pricing, risk management, data analysis, regulatory systems, desktop and web GUIs, web services, algo pricing, end-user scripting"
- 페이스북의 데이터 액세스 도구, 안티스팸 도구
- 금융권의 하스켈 사용: ABN AMRO, Bank of America, Barclays, Credit Suisse, Deutsche Bank, Tsuru Capital

---

## 근데 왜 이렇게 어려운가?

--
- "너 다른 생각 하지 말고 공부만 열심히 해서 좋은 대학 가면 그때부터는 애인도 생기고 하고 싶은 거 마음껏 할 수 있다"

--
- "너 다른 생각 하지 말고 모나드를 배워서 심오한 이치를 깨우치면 그때부터는 하스켈의 쓸모를 마음껏 누릴 수 있다"

--
이런 거 아닙니다

---

class: center, middle

괴담

## 하스켈의 입출력은 뭔가 특이하다/괴상하다/어렵다

---

## 파이선

```python
if __name__ == '__main__':
    print    ('Hello. What is your name?')
    x = input()
    print    ('The input was ' + x)
```

---

## 하스켈

```haskell
main = do
    putStrLn  "Hello. What is your name?"
    x <- getLine
    putStrLn ("The input was " ++ x)
```

--
- ???

---

```python
# -*- coding: utf-8 -*-

def selectiveTransfer(fin, fout):
    line = fin.readline()
    if line == '':
        raise EOFError
    if line.startswith('system:'):
        fout.write(line)
with open('input.txt', 'r') as fin:
    with open('output.txt', 'w') as fout:
        while True:
            try:
                selectiveTransfer(fin, fout)
            except EOFError:
                break
```

---

```haskell
{-# LANGUAGE OverloadedStrings #-}
import Control.Monad (forever)
import qualified Data.ByteString.Char8 as B
import System.IO
import System.IO.Error

selectiveTransfer fin fout = do
    line <- B.hGetLine fin
    if "system:" `B.isPrefixOf` line
        then B.hPutStrLn fout line
        else return ()
main = do
    withFile "input.txt" ReadMode $ \ ihdl ->
        withFile "output.txt" WriteMode $ \ ohdl ->
            untilIOError (selectiveTransfer ihdl ohdl)
untilIOError action = catchIOError (forever action) (\_ -> return ())
```

---

## 입출력 그냥 하면 됩니다.

- 명령형 프로그래밍에서 하던 대로 그냥 하면 잘 됨.
- **Deliberately imperative “look and feel”**
    - Simon Peyton Jones, _[Wearing the hair shirt: a retrospective on Haskell](http://research.microsoft.com/en-us/um/people/simonpj/papers/haskell-retrospective/)_ (2003)
- 일부러 명령형처럼 만들어놨으니 그냥 명령형처럼 쓰라
- 하스켈에서 입출력이 어렵다/특수하다/괴상하다는 오해는 실제로 입출력을 해본 사람들이 해보니까 어렵더라고 말하는 게 아닙니다.
- 모두 단 한 가지 용어로 인해 발생한 것

---

class: center, middle, large

## IO monad

---

## IO Monad Considered Harmful

Justin Le:

> **The phrase “IO monad” considered harmful. Please do not use it**.
>
> ...
>
> I’m going to say that this is probably **the single most harmful and damaging thing** in Haskell ...

--

?!

---

## 유닉스 커맨드

```bash
echo STRING
cat FILENAME
rm FILENAME
mkdir DIRNAME
```

- `echo`나 `cat`은 **커맨드**이고
- `STRING`, `FILENAME`은 **문자열**이자 **커맨드에 들어갈 인자**다.
- **커맨드**와 **문자열**은 서로 다른 **타입**이다.

---

## 유닉스 파이프

```bash
find . | grep "\.txt$"
```

- 한 커맨드의 결과 출력을 다른 커맨드에 입력으로 먹이고 싶다.

--

```bash
cat input.txt | grep "^system:" > output.txt
```

- 아까 파이선/하스켈로 고생고생해서 짰던 코드가 이렇게 쉽게 끝남

---

## 하스켈 커맨드: 액션

```haskell
putStrLn :: String -> IO ()
readFile :: FilePath -> IO String

main = do
    x <- readFile "myname.txt"
    putStrLn ("Hello, " ++ x ++ "!")
```

- `echo`가 문자열 하나를 인자로 받는 커맨드이듯이, `putStrLn`은 `String` 하나를 인자로 받는 액션이다.
- `cat`이 파일 경로를 인자로 받아 파일 내용을 출력하듯이, `readFile`은 파일 경로를 인자로 받아 파일 내용을 문자열로 내놓는 액션이다.
- 액션과 문자열은 서로 다른 타입이다.
- 액션과 `++` 연산자도 서로 다른 타입이다.

---

## 하스켈 파이프

- 하스켈 파이프는 이렇게 생겼습니다: `>>=`

```haskell
main = readFile "myname.txt" >>= putStrLn
```

- 한 커맨드의 출력을 다른 커맨드의 입력으로 먹인다.

---

## 하스켈은 순함수와 액션을 타입으로 구분한다

```haskell
-- pure function
not :: Bool -> Bool
(++) :: [a] -> [a] ->; [a]

-- IO action
getLine :: IO String
putStrLn :: String ->; IO ()
readFile :: FilePath ->; IO String
```

---

## 액션은 이토록 알기 쉬운 개념이다. 그런데

- 유닉스 커맨드를 이해할 수 있다면, 하스켈의 `IO` 액션도 이해할 수 있다.
- 그냥 "`IO` 액션"이나 "`IO` 타입"이라고 부르고, 유닉스 커맨드와 비슷한 거라고 가르치면, 더 이상 설명할 것도 없다.
- 그런데 쓸데없이 IO 모나드라고 부르는 바람에 어마어마하게 오해가 커짐.
- 수많은 초보자들이 "모나드가 뭔가요?"부터 질문하는 암담한 상황. (모르는 단어를 보면 일단 알아야 하는 것이 프로그래머의 본능)
- "하스켈에서 여러 숫자를 나열한 것을 다루려면 뭘 써야 하나요?"
    - "리스트를 쓰시면 됩니다." 혹은 "리스트 타입을 쓰시면 됩니다."
    - 아무도 "리스트 모나드를 쓰시면 됩니다." 같은 괴팍한 답변을 하지는 않는다!
- 따라서 "하스켈에서 입출력을 하려면 뭘 써야 하나요?"에 대한 답변도
    - "IO 타입을 쓰시면 됩니다."가 되어야 한다

---

class: center, middle

> Our biggest mistake: Using the scary term “monad” rather than “warm fuzzy thing”
>
> -- Simon Peyton Jones, _[Wearing the hair shirt: a retrospective on Haskell](http://research.microsoft.com/en-us/um/people/simonpj/papers/haskell-retrospective/)_ (2003)

---

## 역사적 배경

하스켈에 모나드가 언제 처음 들어갔을까요?

--
- 1987년: 위원회 발족. 미랜더를 기반 언어로 선정.
--
 모나드 없음

--
- 1990년: 하스켈 1.0 보고서 발간.
--
 모나드 없음

--
- 1991년: 하스켈 1.1 보고서 발간.
--
 모나드 없음

--
- 1992년: 하스켈 1.2 보고서 발간.
--
 모나드 없음

--
- 1996년: 하스켈 1.3 보고서 발간.

--
 **모나딕 I/O 도입**.

--
    - 모나딕 I/O는 커뮤니티에서 먼저 널리 쓰이고 있었음. (?!)
    - 하스켈 1.3이 이러한 현실을 반영하여 기존의 `[Response] ->; [Request]` I/O를 전면 폐기하고 모나딕 I/O와 `do` 문법을 도입.
--
- 기존의 I/O와 구분하기 위해 "모나딕 I/O", "IO 모나드"라고 부르던 것이 굳어져 비극을 초래

---

## 패망

- 하스켈의 I/O는 모나드가 없어도 되고, 모나드를 몰라도 된다.
- 하스켈에서 모나드라는 타입클래스를 없애버려도 얼마든지 I/O를 계속할 수 있다.
    - 모나드는 인터페이스에 불과하기 때문. `>>=` 함수와 `do` 표기법을 `IO` 타입 전용으로 만들어주면 됨.
- 하스켈에서 **타입클래스를 없애버려도** 얼마든지 I/O를 계속할 수 있다. 타입클래스는 인터페이스에 불과하기 때문.
- 하지만 "`IO` 모나드"라고 부르니까 보자마자 모나드가 뭔지부터 찾게 된다.
    - 그냥 `IO` 타입이라고 했으면 간단히 생략되었을 단계
    - 그야말로 커뮤니티가 야크 셰이빙, "사이드퀘스트"를 권하고 있는 판국

---

class: center, middle

## "하스켈을 쓰려면 모나드를 알아야 한다"

---

## 자바스크립트

```javascript
>>> ['10', '10', '10'].map(parseInt)
```
--
```javascript
[10, NaN, 2]
```

---

class: center

![자바스크립트를 쓰기 위해서 자바스크립트를 알아야 할 필요는 없다.](/static/img/haskell/monad_fear/javascript.jpg)
([Photo by Nathan Smith](https://www.flickr.com/photos/nathansmith/4704268314/in/photostream/). Released under the [Creative Commons Attribution 2.0](https://creativecommons.org/licenses/by/2.0/) license.)

--

자바스크립트를 쓰기 위해서 자바스크립트를 알아야 할 필요는 없듯이하스켈을 쓰기 위해서 모나드를 알아야 할 필요는 없다

---

class: center

## 모든 `do` 표기법 코드는 모나드로 번역된다.그러니 모나드는 필수 개념이 아닌가?

--

얼핏 보면, 맞는 말 같지만...

---

class: center

## 모든 C/C++ 코드는 어셈블리로 번역된다.따라서 C/C++를 배우기 위해서는어셈블리를 먼저 배워야 한다.

--

... 이렇게 바꿔 보면 그렇지만은 않다는 것을 알 수 있다.

---

## 셈하기

(출처: [Why I won't be writing a monad tutorial](http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/) by scottw.)

--
- 어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.

--
- 고양이 두 마리가 있다.

--
- 강아지 두 마리가 있다.

--
- 말 두 마리가 있다.

--
- "뭐가 똑같은지 알겠니?"

--
- "똑같은 게 없어요!"

---

## 셈하기

- "아니야, 공통점이 있단다. 뭔지 모르겠니?"

--
- "다 달라요! 고양이랑 강아지랑 달라요. 고양이랑 말이랑 달라요."

--
- "그럼 이렇게 생각해 보렴. 집합 S는 모든 T ∈ S에 관하여 T ⊂ S이고 S의 원소들의 포함 관계인 ⊂ 는 전순서를 이룬다고 가정하자."

--
- 앨리스는 울음을 터뜨린다.

---

## 과일이란 무엇인가?

- 과일이 무엇인지 모르는 사람에게 "과일이란 무엇인가?"을 가르칠 때
    - 사과도 과일이다.
    - 귤도 과일이다.
    - 배도 과일이다.
    - ...
- 과일이란 식물을 가꾸었을 때 그 식물이 번식의 수단으로서 형성하는, 사람이 먹을 수 있는 열매의 총칭으로서 주로 종자와 과육이 붙어 있는 구조로 이루어져 있으며 대개 수분 과즙이 많고 단맛 또는 신맛이 난다.
    - 이러지 않습니다.
- 구체적인 사례로부터 추상적인 개념을 유도하는 것이 우리가 직관적으로 알고 있는 교수법적 상식이다.

---

## 설령 이해하더라도...

- 모나드라는 개념을 이해하는 것과, 모나드인 타입들(`IO`, `ST`, `[]`, `Maybe`, ...)을 사용하는 실무적 능력은 별개의 문제다.
- 범주론에서 말하는 모나드와 하스켈의 모나드는 또 조금씩 다르다.

--

> 모나드가 무엇인지 이해함으로써 하스켈 프로그래머가 되겠다는 것은 "악기란 무엇인가?"를 이해하면 모든 악기의 연주자가 될 수 있으리라는 믿음과 같다.
> Attempting to learn how to use monads by understanding what they are is like asking "What is a musical instrument?" and then assuming once you know the answer to that, you'll be able to play all of the musical instruments.
> ~kqr, _[The "What Are Monads?" Fallacy](http://two-wrongs.com/the-what-are-monads-fallacy)_ (2015)

---

## 그래서 무슨 일이 생기는가

--
- 초보자는 모나드를 반드시 이해해야 한다고 생각함

--
- 이해하지 못함
--
 (대개 여기서 포기)

--
- 어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다

--
- 어느 순간 모나드가 무엇인지 이해하게 됨

--
- 그러자 갑자기 모든 것이 쉽게 느껴짐

--
- 이 깨달음을 세상에 널리 퍼뜨려 중생을 제도하겠다고 마음먹음

--
- 세상에는 모나드 튜토리얼 하나가 더 추가됨
--
 (이미 셀 수도 없이 많다)

---

## 모나드 튜토리얼

--
> A 'newbie', in Haskell, is someone who hasn't yet implemented a compiler. They've only written a monad tutorial.
> [Pseudonym](http://sequence.complete.org/hwn/20061122)

--

- 모나드 튜토리얼을 쓰는 방법에 대한 튜토리얼
    - tora, _[My how to give a 'monad tutorial' tutorial](http://www.doc.ic.ac.uk/~tora/monadsI.txt)_ (2010)
    - Travis Hance, _[Write you a monad tutorial](https://tjhance.quora.com/Write-you-a-monad-tutorial)_ (2014)

---

## 모나드란

- 모나드는 **타입 클래스**입니다.
- 타입 클래스는 **타입**의 집합입니다.
- 타입은 **값**의 집합입니다.
- 하스켈에서 모나드는 공통점이 있는 여러 개의 타입에 대해서 만들어 놓은 공통의 인터페이스를 말합니다.
- 따라서, 어떤 타입이 모나드에 속한다고 해도, 다른 모나딕 타입들과는 전혀 상관이 없어 보일 수도 있음.

---

## 따라서 모나드를 배우기 위해서는

--
- 먼저 `IO` 타입을 써본다.

--
- 그리고 `Maybe` 타입도 써본다.

--
- 그리고 리스트 타입도 써본다.

--
- 하스켈 코드를 많이 작성해 본다. (1천 줄?)

--
- 그러다가 어느 순간 이것들이 가지고 있는 공통점에 대해서 알게 된다. (Aha moment)

--
- 하지만 계속 몰라도 별 상관 없다.

--
- **모나드가 무엇인지 따로 배우려고 하지 않는다.**
--
 좌절감과 혼란을 초래할 뿐이다.

---

class: center, middle

## "아, 나도 하스켈 하려고 해봤는데, 모나드 때문에..."

---

class: center, middle

## 이제는 사라져야

---

## "하스켈은 어렵다"

정확히 말하면,

> 다른 언어들(C/C++, 자바, C#, 자바스크립트, 파이선, ...)에 비해 **특별히** 어려운 데가 있을 것이다.

---

## 어려움의 종류

- 배우기 어렵다
- 쓰기 어렵다

--
- 배우기는 쉬운데 쓰기는 어려운 언어가 있습니다.
--
 어셈블리

---

## 하스켈은 "배우기" 어렵다

- 온갖 음해에 시달렸습니다 여러분.
- 페다고지, 교수법의 실패
- 그냥 쓰면 써짐

---

## 하스켈은 "쓰기" 어렵다.

- 참조 투명성
- 불변성
- 재귀

--

(어렵다기보다는 불편한 것)

--

- 입출력은 쓰기 어려운 것에 속하지 않는다. 쉽다.

---

## 참조 투명성과 불변성

- 가변 자료를 짓주무르는 방식이 빠른 스크립팅에서 더 편하긴 하다
- 그러나 stateful한 코드는 코드가 커질수록 치명적인 독이 됨
- stateful한 코드는 디버그 하기도 골치아프다.
- 가변 자료 쓰는 스크립트 언어라도 프로젝트가 되면 MVC 모델 등 state 분리하는 접근이 권장됨
- 가변 자료를 짓주무르는 코드는 병렬화도 할 수 없다
- 결국 지향점이 다른 것. 한번 쓰고 버릴 코드라면 가변 자료 쓰는 스크립팅 언어가 더 편하고 빠르고 좋을 것이다

---

## 나는 그래도 가변 자료 하고 싶다!

- 하스켈에도 가변 자료형 있습니다.
- `ST` 액션과 `STRef`, `STArray`, `STUArray` 타입을 쓰시면 됩니다.

---

## 재귀

- 하스켈 처음 배울 때 제가 가장 헷갈렸던 것
- 같은 코드에 여러 문맥이 중첩되어 있고, 그게 `for`와 달리 `i` 하나만 바뀌는 게 아니다
- 익숙해지고 나니 전혀 불편하지 않은데, 익숙해지는 비용은 있을 것이다

---

## 재귀가 싫으면 그냥 `for` 씁시다.

- 하스켈에도 `for` 있습니다.

--

```haskell
import Control.Monad

main :: IO ()
main = forM_ [1 .. 10] $ \ i -> do
    print i
```

- 코드 생긴 것도 다른 언어의 `for`와 똑같음.
- "이 이상 좋게 해 줄 수 없다."

---

## 하스켈은 수학적인 언어다

- 왜냐하면 용어가 수학적이고

![Typeclassopedia](/static/img/haskell/monad_fear/Typeclassopedia-diagram.png)

(From _Typeclassopedia_ by Brent Yorgey. Originally published 12 March 2009 in issue 13 of the _Monad.Reader_)

- 타입 이론 연구 등에 사용되고 있기 때문이다.

---

## 이것은 마치

--
- 수많은 냥짤이 JPEG로 저장되어 있다.

--
- JPEG는 고양이적인 포맷이다.

--
- ?!

--
- 하스켈의 공식 목표 중에 "수학적 언어"는 없지만 "애플리케이션 개발에 쓸 수 있는 언어"는 있다

--
- 범주론은 초기 하스켈에는 아예 없었다

--
- 하스켈을 "수학적인 언어"라고 부르는 것은 하스켈의 이론적 완성도를 칭송하려는 의도도 있지만, 초보자에게 겁을 주는 역효과도 있다.

--
- 진짜 "수학적인 언어"는 따로 있다. Mathematica, Maple, ...

---

## 결론

--

- 하스켈 어렵지 않다.

--
- 하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)

--
- 모나드를 몰라도 하스켈을 쓸 수 있다

--
    - 모나드를 몰라도 _실용적_ 하스켈을 쓸 수 있다
--
- 하스켈을 배우기 위해서 수학을 잘 해야 되는 것은 아니다

--
- 하스켈 쓰면서 모나드를 모르고 살아도 된다

--
- "모나드 때문에 하스켈 포기" = "어셈블리 때문에 C 포기"

--
- 더 이상 이런 불행이 없었으면.

---

class: center, middle

## 감사합니다.


</textarea>
<script src="./모나드 괴담_files/remark-latest.min.js" type="application/javascript"></script>
<script type="application/javascript">
var slideshow = remark.create({
    ratio: '16:9',
    countIncrementalSlides: false
})
</script><div class="remark-notes-area">
  <div class="remark-top-area">
    <div class="remark-toolbar">
      <a class="remark-toolbar-link" href="https://xtendo.org/ko/monad#increase">+</a>
      <a class="remark-toolbar-link" href="https://xtendo.org/ko/monad#decrease">-</a>
      <span class="remark-toolbar-timer">0:11:41</span>
    </div>
  </div>
  <div class="remark-bottom-area">
    <div class="remark-notes-current-area">
      <div class="remark-toggle">Notes for current slide</div>
      <div class="remark-notes"></div>
    </div>
    <div class="remark-notes-preview-area">
      <div class="remark-toggle">Notes for next slide</div>
      <div class="remark-notes-preview"></div>
    </div>
  </div>
</div>
<div class="remark-slides-area"><div class="remark-slide-container remark-visible"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">모나드 괴담</h2>
<p>엑스티<br>
2015년 11월 14일</p><div class="remark-slide-number">1 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-del-del-"><del>온갖 음해에 시달렸습니다</del></h2>
<ul>
<li>하스켈은 어렵다</li>
<li>모나드가 어려워서 하스켈은 어렵다</li>
<li>모나드를 알아야 하스켈을 쓸 수 있다<ul>
<li>모나드를 알아야 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈은 수학적인 언어다</li>
<li>아무튼 모나드를 배워야 한다</li>
</ul><div class="remark-slide-number">2 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-del-del-"><del>온갖 음해에 시달렸습니다</del></h2>
<ul>
<li>하스켈은 어렵다</li>
<li>모나드가 어려워서 하스켈은 어렵다</li>
<li>모나드를 알아야 하스켈을 쓸 수 있다<ul>
<li>모나드를 알아야 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈은 수학적인 언어다</li>
<li>아무튼 모나드를 배워야 한다</li>
</ul>
<p><strong>NO</strong></p><div class="remark-slide-number">2 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">저 혼자만의 생각이 아닙니다.</h2>
<ul>
<li>Dan Piponi, <em><a href="http://blog.sigfpe.com/2007/11/io-monad-for-people-who-simply-dont.html">The IO Monad for People who Simply Don't Care</a></em> (2007)</li>
<li>Brent Yorgey, <em><a href="https://byorgey.wordpress.com/2009/01/12/abstraction-intuition-and-the-monad-tutorial-fallacy/">Abstraction, intuition, and the “monad tutorial fallacy”</a></em> (2009)</li>
<li>tora, <em><a href="http://www.doc.ic.ac.uk/~tora/monadsI.txt">My how to give a 'monad tutorial' tutorial</a></em> (2010)</li>
<li>scottw, <em><a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a></em> (2013)</li>
<li>Travis Hance, <em><a href="https://tjhance.quora.com/Write-you-a-monad-tutorial">Write you a monad tutorial</a></em> (2014)</li>
<li>~kqr, <em><a href="http://two-wrongs.com/the-what-are-monads-fallacy">The "What Are Monads?" Fallacy</a></em> (2015)</li>
<li>Justin Le, <em><a href="http://blog.jle.im/entry/io-monad-considered-harmful">IO Monad Considered Harmful</a></em> (2015)</li>
</ul>
<p>"왜 무수한 하스켈 초보자들이 똑같은 (잘못된) 질문을 하고, 똑같은 (겪지 않아도 될) 어려움을 겪는 것일까?"에 대한 문제의식이 최근 몇 년간 형성되기 시작함</p><div class="remark-slide-number">3 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="1-">1년 가까이 하스켈 모임을 운영해보니...</h2>
<p>독보적으로 많이 들은 이야기 1위</p><div class="remark-slide-number">4 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">모나드가 뭐죠?</h2><div class="remark-slide-number">5 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">모나드가 뭐죠?</h2>
<p>...는 아니고요</p><div class="remark-slide-number">5 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">하스켈이 그렇게 좋은 언어라면 왜 많이들 안 쓰나요?</h2><div class="remark-slide-number">6 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><p><img src="./모나드 괴담_files/facepalm.jpg" alt="facepalm"></p>
<p>(<a href="http://www.flickr.com/photos/proimos/4199675334/">Photo</a> by <a href="http://www.flickr.com/photos/proimos/">Alex E. Proimos</a>. Released under the <a href="https://creativecommons.org/licenses/by/2.0/deed.en">Creative Commons Attribution 2.0 Generic</a> license.)</p><div class="remark-slide-number">7 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">물론 하스켈만의 이유가 있기는 합니다.</h2>
<ul>
<li>"Avoid success at all cost": 성공하면 하위호환성을 깰 수 없다. 성공하지 말고 계속 혁신하자</li>
<li>하스켈에서 성공적으로 검증된 개념이 다른 언어에 받아들여지는 사례 증가<ul>
<li>파이선의 List comprehension</li>
<li>러스트의 Trait, C++의 Concept, 자바의 저네릭스</li>
<li>Maybe chain</li>
<li>...</li>
</ul>
</li>
<li>스스로 성공하지 않되 다른 모든 프로그래밍 언어의 발전을 선도하는 언어</li>
<li>그럼에도, 최근 상업적으로 상당한 쓰임을 보이고 있음</li>
<li>아무튼, 오늘 하려는 얘기는...</li>
</ul><div class="remark-slide-number">8 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">모나드를 이해해 보려고 했는데 너무 어렵더라고요.</h2><div class="remark-slide-number">9 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">하스켈 너무 어려워요. 무슨 말인지 하나도 모르겠어요.</h2><div class="remark-slide-number">10 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
<li>대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들</li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
<li>대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들</li>
<li><strong>모르는 것을 설명하기 위해서 모르는 개념을 동원한다</strong></li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
<li>대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들</li>
<li><strong>모르는 것을 설명하기 위해서 모르는 개념을 동원한다</strong></li>
<li>?!</li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
<li>대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들</li>
<li><strong>모르는 것을 설명하기 위해서 모르는 개념을 동원한다</strong></li>
<li>?!</li>
<li>어렵다고 난리가 날 수밖에...</li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">광범위한 교수법적 실패</h2>
<ul>
<li>"하스켈이란 무엇인가?"로 찾아보면<ul>
<li>순함수형(purely functional) 프로그래밍 언어다.</li>
<li>게으른(lazy) 언어다.</li>
<li>모나드(monad)를 쓴다.</li>
<li>타입클래스(typeclass).</li>
<li>기타 등등.</li>
</ul>
</li>
<li>대체로, 하스켈을 처음 접하는 사람들이 알 리가 없는 것들</li>
<li><strong>모르는 것을 설명하기 위해서 모르는 개념을 동원한다</strong></li>
<li>?!</li>
<li>어렵다고 난리가 날 수밖에... ㅠㅠ</li>
</ul><div class="remark-slide-number">11 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">하스켈이라는 언어는 왜 만들어졌는가?</h2><div class="remark-slide-number">12 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="haskell-2010-report">Haskell 2010 Report</h2>
<h3 id="preface">Preface</h3>
<p>[...]</p>
<h4 id="goals">Goals</h4>
<blockquote>
<ol>
<li>It should be suitable for teaching, research, and <strong>applications, including building large systems</strong>.</li>
</ol>
</blockquote><div class="remark-slide-number">13 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="haskell-2010-report">Haskell 2010 Report</h2>
<h3 id="preface">Preface</h3>
<p>[...]</p>
<h4 id="goals">Goals</h4>
<blockquote>
<ol>
<li>It should be suitable for teaching, research, and <strong>applications, including building large systems</strong>.</li>
</ol>
</blockquote>
<ul>
<li>언어 설계의 목표 가운데 애플리케이션 개발용으로 적합하여야 한다는 요건이 명기되어 있다.</li>
</ul><div class="remark-slide-number">13 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2>
<ul>
<li>1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다</li>
</ul><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2>
<ul>
<li>1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다</li>
<li>선택지가 너무 많아서 노력이 분산되고, 시장에서는 하나도 선택받지 못하는 상황</li>
</ul><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2>
<ul>
<li>1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다</li>
<li>선택지가 너무 많아서 노력이 분산되고, 시장에서는 하나도 선택받지 못하는 상황</li>
<li>순함수형이 좋은 생각 같은데 더 널리 쓰이지 못하니 안타깝다. 그러니 하나로 뭉쳐 <strong>선택받는 언어를 만들어보자.</strong></li>
</ul><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2>
<ul>
<li>1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다</li>
<li>선택지가 너무 많아서 노력이 분산되고, 시장에서는 하나도 선택받지 못하는 상황</li>
<li>순함수형이 좋은 생각 같은데 더 널리 쓰이지 못하니 안타깝다. 그러니 하나로 뭉쳐 <strong>선택받는 언어를 만들어보자.</strong></li>
<li>즉, <strong>학술 연구 전용 언어가 아니다.</strong></li>
</ul><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 위원회가 조직된 배경</h2>
<ul>
<li>1987년 당시 넌스트릭트 순함수형 언어가 난립하고 있었다</li>
<li>선택지가 너무 많아서 노력이 분산되고, 시장에서는 하나도 선택받지 못하는 상황</li>
<li>순함수형이 좋은 생각 같은데 더 널리 쓰이지 못하니 안타깝다. 그러니 하나로 뭉쳐 <strong>선택받는 언어를 만들어보자.</strong></li>
<li>즉, <strong>학술 연구 전용 언어가 아니다.</strong></li>
<li><strong>현실에서 쓰이겠다는 목표를 가지고 만들어졌다</strong>.</li>
</ul><div class="remark-slide-number">14 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 현실의 문제를 해결하는 현실의 도구입니다</h2>
<ul>
<li>C보다 고성능인 웹 서버</li>
<li>스탠다드 차타드: "real time pricing, risk management, data analysis, regulatory systems, desktop and web GUIs, web services, algo pricing, end-user scripting"</li>
<li>페이스북의 데이터 액세스 도구, 안티스팸 도구</li>
<li>금융권의 하스켈 사용: ABN AMRO, Bank of America, Barclays, Credit Suisse, Deutsche Bank, Tsuru Capital</li>
</ul><div class="remark-slide-number">15 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">근데 왜 이렇게 어려운가?</h2><div class="remark-slide-number">16 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">근데 왜 이렇게 어려운가?</h2>
<ul>
<li>"너 다른 생각 하지 말고 공부만 열심히 해서 좋은 대학 가면 그때부터는 애인도 생기고 하고 싶은 거 마음껏 할 수 있다"</li>
</ul><div class="remark-slide-number">16 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">근데 왜 이렇게 어려운가?</h2>
<ul><
<li>"너 다른 생각 하지 말고 공부만 열심히 해서 좋은 대학 가면 그때부터는 애인도 생기고 하고 싶은 거 마음껏 할 수 있다"</li>
<li>"너 다른 생각 하지 말고 모나드를 배워서 심오한 이치를 깨우치면 그때부터는 하스켈의 쓸모를 마음껏 누릴 수 있다"</li>
</ul><div class="remark-slide-number">16 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">근데 왜 이렇게 어려운가?</h2>
<ul>
<li>"너 다른 생각 하지 말고 공부만 열심히 해서 좋은 대학 가면 그때부터는 애인도 생기고 하고 싶은 거 마음껏 할 수 있다"</li>
<li>"너 다른 생각 하지 말고 모나드를 배워서 심오한 이치를 깨우치면 그때부터는 하스켈의 쓸모를 마음껏 누릴 수 있다"</li>
<li><del>이런 거 아닙니다</del></li>
</ul><div class="remark-slide-number">16 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><p>괴담</p>
<h2 id="-">하스켈의 입출력은 뭔가 특이하다/괴상하다/어렵다</h2><div class="remark-slide-number">17 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">파이선</h2>
<pre><code class="python hljs remark-code"><div class="remark-code-line"><span class="hljs-keyword">if</span> __name__ == <span class="hljs-string">'__main__'</span>:</div><div class="remark-code-line">    <span class="hljs-keyword">print</span>    (<span class="hljs-string">'Hello. What is your name?'</span>)</div><div class="remark-code-line">    x = input()</div><div class="remark-code-line">    <span class="hljs-keyword">print</span>    (<span class="hljs-string">'The input was '</span> + x)</div></code></pre><div class="remark-slide-number">18 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈</h2>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-title">main</span> = <span class="hljs-keyword">do</span></div><div class="remark-code-line">    putStrLn  <span class="hljs-string">"Hello. What is your name?"</span></div><div class="remark-code-line">    x <- getLine</div><div class="remark-code-line">    putStrLn (<span class="hljs-string">"The input was "</span> ++ x)</div></code></pre><div class="remark-slide-number">19 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈</h2>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-title">main</span> = <span class="hljs-keyword">do</span></div><div class="remark-code-line">    putStrLn  <span class="hljs-string">"Hello. What is your name?"</span></div><div class="remark-code-line">    x <- getLine</div><div class="remark-code-line">    putStrLn (<span class="hljs-string">"The input was "</span> ++ x)</div></code></pre>
<ul>
<li>???</li>
</ul><div class="remark-slide-number">19 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><pre><code class="python hljs remark-code"><div class="remark-code-line"><span class="hljs-comment"># -*- coding: utf-8 -*-</span></div><div class="remark-code-line"></div><div class="remark-code-line"><span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">selectiveTransfer</span><span class="hljs-params">(fin, fout)</span>:</span></div><div class="remark-code-line">    line = fin.readline()</div><div class="remark-code-line">    <span class="hljs-keyword">if</span> line == <span class="hljs-string">''</span>:</div><div class="remark-code-line">        <span class="hljs-keyword">raise</span> EOFError</div><div class="remark-code-line">    <span class="hljs-keyword">if</span> line.startswith(<span class="hljs-string">'system:'</span>):</div><div class="remark-code-line">        fout.write(line)</div><div class="remark-code-line"><span class="hljs-keyword">with</span> open(<span class="hljs-string">'input.txt'</span>, <span class="hljs-string">'r'</span>) <span class="hljs-keyword">as</span> fin:</div><div class="remark-code-line">    <span class="hljs-keyword">with</span> open(<span class="hljs-string">'output.txt'</span>, <span class="hljs-string">'w'</span>) <span class="hljs-keyword">as</span> fout:</div><div class="remark-code-line">        <span class="hljs-keyword">while</span> <span class="hljs-keyword">True</span>:</div><div class="remark-code-line">            <span class="hljs-keyword">try</span>:</div><div class="remark-code-line">                selectiveTransfer(fin, fout)</div><div class="remark-code-line">            <span class="hljs-keyword">except</span> EOFError:</div><div class="remark-code-line">                <span class="hljs-keyword">break</span></div></code></pre><div class="remark-slide-number">20 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-meta">{-# LANGUAGE OverloadedStrings #-}</span></div><div class="remark-code-line"><span class="hljs-keyword">import</span> Control.Monad (<span class="hljs-title">forever</span>)</div><div class="remark-code-line"><span class="hljs-keyword">import</span> <span class="hljs-keyword">qualified</span> Data.ByteString.Char8 <span class="hljs-keyword">as</span> B</div><div class="remark-code-line"><span class="hljs-keyword">import</span> System.IO</div><div class="remark-code-line"><span class="hljs-keyword">import</span> System.IO.Error</div><div class="remark-code-line"></div><div class="remark-code-line"><span class="hljs-title">selectiveTransfer</span> fin fout = <span class="hljs-keyword">do</span></div><div class="remark-code-line">    line <- <span class="hljs-type">B</span>.hGetLine fin</div><div class="remark-code-line">    <span class="hljs-keyword">if</span> <span class="hljs-string">"system:"</span> `<span class="hljs-type">B</span>.isPrefixOf` line</div><div class="remark-code-line">        <span class="hljs-keyword">then</span> <span class="hljs-type">B</span>.hPutStrLn fout line</div><div class="remark-code-line">        <span class="hljs-keyword">else</span> return ()</div><div class="remark-code-line"><span class="hljs-title">main</span> = <span class="hljs-keyword">do</span></div><div class="remark-code-line">    withFile <span class="hljs-string">"input.txt"</span> <span class="hljs-type">ReadMode</span> $ \ ihdl -></div><div class="remark-code-line">        withFile <span class="hljs-string">"output.txt"</span> <span class="hljs-type">WriteMode</span> $ \ ohdl -></div><div class="remark-code-line">            untilIOError (selectiveTransfer ihdl ohdl)</div><div class="remark-code-line"><span class="hljs-title">untilIOError</span> action = catchIOError (forever action) (\_ -> return ())</div></code></pre><div class="remark-slide-number">21 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">입출력 그냥 하면 됩니다.</h2>
<ul>
<li>명령형 프로그래밍에서 하던 대로 그냥 하면 잘 됨.</li>
<li><strong>Deliberately imperative “look and feel”</strong><ul>
<li>Simon Peyton Jones, <em><a href="http://research.microsoft.com/en-us/um/people/simonpj/papers/haskell-retrospective/">Wearing the hair shirt: a retrospective on Haskell</a></em> (2003)</li>
</ul>
</li>
<li>일부러 명령형처럼 만들어놨으니 그냥 명령형처럼 쓰라</li>
<li>하스켈에서 입출력이 어렵다/특수하다/괴상하다는 오해는 실제로 입출력을 해본 사람들이 해보니까 어렵더라고 말하는 게 아닙니다.</li>
<li>모두 단 한 가지 용어로 인해 발생한 것</li>
</ul><div class="remark-slide-number">22 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle large hljs-default"><h2 id="io-monad">IO monad</h2><div class="remark-slide-number">23 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="io-monad-considered-harmful">IO Monad Considered Harmful</h2>
<p>Justin Le:</p>
<blockquote>
<p><strong>The phrase “IO monad” considered harmful. Please do not use it</strong>.</p>
<p>...</p>
<p>I’m going to say that this is probably <strong>the single most harmful and damaging thing</strong> in Haskell ...</p>
</blockquote><div class="remark-slide-number">24 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="io-monad-considered-harmful">IO Monad Considered Harmful</h2>
<p>Justin Le:</p>
<blockquote>
<p><strong>The phrase “IO monad” considered harmful. Please do not use it</strong>.</p>
<p>...</p>
<p>I’m going to say that this is probably <strong>the single most harmful and damaging thing</strong> in Haskell ...</p>
</blockquote>
<p>?!</p><div class="remark-slide-number">24 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">유닉스 커맨드</h2>
<pre><code class="bash hljs remark-code"><div class="remark-code-line"><span class="hljs-built_in">echo</span> STRING</div><div class="remark-code-line">cat FILENAME</div><div class="remark-code-line">rm FILENAME</div><div class="remark-code-line">mkdir DIRNAME</div></code></pre>
<ul>
<li><code class="remark-inline-code">echo</code>나 <code class="remark-inline-code">cat</code>은 <strong>커맨드</strong>이고</li>
<li><code class="remark-inline-code">STRING</code>, <code class="remark-inline-code">FILENAME</code>은 <strong>문자열</strong>이자 <strong>커맨드에 들어갈 인자</strong>다.</li>
<li><strong>커맨드</strong>와 <strong>문자열</strong>은 서로 다른 <strong>타입</strong>이다.</li>
</ul><div class="remark-slide-number">25 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">유닉스 파이프</h2>
<pre><code class="bash hljs remark-code"><div class="remark-code-line">find . | grep <span class="hljs-string">"\.txt$"</span></div></code></pre>
<ul>
<li>한 커맨드의 결과 출력을 다른 커맨드에 입력으로 먹이고 싶다.</li>
</ul><div class="remark-slide-number">26 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">유닉스 파이프</h2>
<pre><code class="bash hljs remark-code"><div class="remark-code-line">find . | grep <span class="hljs-string">"\.txt$"</span></div></code></pre>
<ul>
<li>한 커맨드의 결과 출력을 다른 커맨드에 입력으로 먹이고 싶다.</li>
</ul>
<pre><code class="bash hljs remark-code"><div class="remark-code-line">cat input.txt | grep <span class="hljs-string">"^system:"</span> > output.txt</div></code></pre>
<ul>
<li>아까 파이선/하스켈로 고생고생해서 짰던 코드가 이렇게 쉽게 끝남</li>
</ul><div class="remark-slide-number">26 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 커맨드: 액션</h2>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-title">putStrLn</span> :: <span class="hljs-type">String</span> -> <span class="hljs-type">IO</span> ()</div><div class="remark-code-line"><span class="hljs-title">readFile</span> :: <span class="hljs-type">FilePath</span> -> <span class="hljs-type">IO</span> <span class="hljs-type">String</span></div><div class="remark-code-line"></div><div class="remark-code-line"><span class="hljs-title">main</span> = <span class="hljs-keyword">do</span></div><div class="remark-code-line">    x <- readFile <span class="hljs-string">"myname.txt"</span></div><div class="remark-code-line">    putStrLn (<span class="hljs-string">"Hello, "</span> ++ x ++ <span class="hljs-string">"!"</span>)</div></code></pre>
<ul>
<li><code class="remark-inline-code">echo</code>가 문자열 하나를 인자로 받는 커맨드이듯이, <code class="remark-inline-code">putStrLn</code>은 <code class="remark-inline-code">String</code> 하나를 인자로 받는 액션이다.</li>
<li><code class="remark-inline-code">cat</code>이 파일 경로를 인자로 받아 파일 내용을 출력하듯이, <code class="remark-inline-code">readFile</code>은 파일 경로를 인자로 받아 파일 내용을 문자열로 내놓는 액션이다.</li>
<li>액션과 문자열은 서로 다른 타입이다.</li>
<li>액션과 <code class="remark-inline-code">++</code> 연산자도 서로 다른 타입이다.</li>
</ul><div class="remark-slide-number">27 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈 파이프</h2>
<ul>
<li>하스켈 파이프는 이렇게 생겼습니다: <code class="remark-inline-code">>>=</code></li>
</ul>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-title">main</span> = readFile <span class="hljs-string">"myname.txt"</span> >>= putStrLn</div></code></pre>
<ul>
<li>한 커맨드의 출력을 다른 커맨드의 입력으로 먹인다.</li>
</ul><div class="remark-slide-number">28 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 순함수와 액션을 타입으로 구분한다</h2>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-comment">-- pure function</span></div><div class="remark-code-line"><span class="hljs-title">not</span> :: <span class="hljs-type">Bool</span> -> <span class="hljs-type">Bool</span></div><div class="remark-code-line">(++) :: [a] -> [a] -> [a]</div><div class="remark-code-line"></div><div class="remark-code-line"><span class="hljs-comment">-- IO action</span></div><div class="remark-code-line"><span class="hljs-title">getLine</span> :: <span class="hljs-type">IO</span> <span class="hljs-type">String</span></div><div class="remark-code-line"><span class="hljs-title">putStrLn</span> :: <span class="hljs-type">String</span> -> <span class="hljs-type">IO</span> ()</div><div class="remark-code-line"><span class="hljs-title">readFile</span> :: <span class="hljs-type">FilePath</span> -> <span class="hljs-type">IO</span> <span class="hljs-type">String</span></div></code></pre><div class="remark-slide-number">29 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">액션은 이토록 알기 쉬운 개념이다. 그런데</h2>
<ul>
<li>유닉스 커맨드를 이해할 수 있다면, 하스켈의 <code class="remark-inline-code">IO</code> 액션도 이해할 수 있다.</li>
<li>그냥 "<code class="remark-inline-code">IO</code> 액션"이나 "<code class="remark-inline-code">IO</code> 타입"이라고 부르고, 유닉스 커맨드와 비슷한 거라고 가르치면, 더 이상 설명할 것도 없다.</li>
<li>그런데 쓸데없이 IO 모나드라고 부르는 바람에 어마어마하게 오해가 커짐.</li>
<li>수많은 초보자들이 "모나드가 뭔가요?"부터 질문하는 암담한 상황. (모르는 단어를 보면 일단 알아야 하는 것이 프로그래머의 본능)</li>
<li>"하스켈에서 여러 숫자를 나열한 것을 다루려면 뭘 써야 하나요?"<ul>
<li>"리스트를 쓰시면 됩니다." 혹은 "리스트 타입을 쓰시면 됩니다."</li>
<li>아무도 "리스트 모나드를 쓰시면 됩니다." 같은 괴팍한 답변을 하지는 않는다!</li>
</ul>
</li>
<li>따라서 "하스켈에서 입출력을 하려면 뭘 써야 하나요?"에 대한 답변도<ul>
<li>"IO 타입을 쓰시면 됩니다."가 되어야 한다</li>
</ul>
</li>
</ul><div class="remark-slide-number">30 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><blockquote>
<p>Our biggest mistake: Using the scary term “monad” rather than “warm fuzzy thing”</p>
<p>-- Simon Peyton Jones, <em><a href="http://research.microsoft.com/en-us/um/people/simonpj/papers/haskell-retrospective/">Wearing the hair shirt: a retrospective on Haskell</a></em> (2003)</p>
</blockquote><div class="remark-slide-number">31 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간. 모나드 없음</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간. 모나드 없음</li>
<li>1996년: 하스켈 1.3 보고서 발간.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간. 모나드 없음</li>
<li>1996년: 하스켈 1.3 보고서 발간.
<strong>모나딕 I/O 도입</strong>.</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간. 모나드 없음</li>
<li>1996년: 하스켈 1.3 보고서 발간.
<strong>모나딕 I/O 도입</strong>.<ul>
<li>모나딕 I/O는 커뮤니티에서 먼저 널리 쓰이고 있었음. (?!)</li>
<li>하스켈 1.3이 이러한 현실을 반영하여 기존의 <code class="remark-inline-code">[Response] -> [Request]</code> I/O를 전면 폐기하고 모나딕 I/O와 <code class="remark-inline-code">do</code> 문법을 도입.</li>
</ul>
</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">역사적 배경</h2>
<p>하스켈에 모나드가 언제 처음 들어갔을까요?</p>
<ul>
<li>1987년: 위원회 발족. 미랜더를 기반 언어로 선정. 모나드 없음</li>
<li>1990년: 하스켈 1.0 보고서 발간. 모나드 없음</li>
<li>1991년: 하스켈 1.1 보고서 발간. 모나드 없음</li>
<li>1992년: 하스켈 1.2 보고서 발간. 모나드 없음</li>
<li>1996년: 하스켈 1.3 보고서 발간.
<strong>모나딕 I/O 도입</strong>.<ul>
<li>모나딕 I/O는 커뮤니티에서 먼저 널리 쓰이고 있었음. (?!)</li>
<li>하스켈 1.3이 이러한 현실을 반영하여 기존의 <code class="remark-inline-code">[Response] -> [Request]</code> I/O를 전면 폐기하고 모나딕 I/O와 <code class="remark-inline-code">do</code> 문법을 도입.</li>
</ul>
</li>
<li>기존의 I/O와 구분하기 위해 "모나딕 I/O", "IO 모나드"라고 부르던 것이 굳어져 비극을 초래</li>
</ul><div class="remark-slide-number">32 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">패망</h2>
<ul>
<li>하스켈의 I/O는 모나드가 없어도 되고, 모나드를 몰라도 된다.</li>
<li>하스켈에서 모나드라는 타입클래스를 없애버려도 얼마든지 I/O를 계속할 수 있다.<ul>
<li>모나드는 인터페이스에 불과하기 때문. <code class="remark-inline-code">>>=</code> 함수와 <code class="remark-inline-code">do</code> 표기법을 <code class="remark-inline-code">IO</code> 타입 전용으로 만들어주면 됨.</li>
</ul>
</li>
<li>하스켈에서 <strong>타입클래스를 없애버려도</strong> 얼마든지 I/O를 계속할 수 있다. 타입클래스는 인터페이스에 불과하기 때문.</li>
<li>하지만 "<code class="remark-inline-code">IO</code> 모나드"라고 부르니까 보자마자 모나드가 뭔지부터 찾게 된다.<ul>
<li>그냥 <code class="remark-inline-code">IO</code> 타입이라고 했으면 간단히 생략되었을 단계</li>
<li>그야말로 커뮤니티가 야크 셰이빙, "사이드퀘스트"를 권하고 있는 판국</li>
</ul>
</li>
</ul><div class="remark-slide-number">33 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">"하스켈을 쓰려면 모나드를 알아야 한다"</h2><div class="remark-slide-number">34 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">자바스크립트</h2>
<pre><code class="javascript hljs remark-code"><div class="remark-code-line">>>> [<span class="hljs-string">'10'</span>, <span class="hljs-string">'10'</span>, <span class="hljs-string">'10'</span>].map(<span class="hljs-built_in">parseInt</span>)</div></code></pre><div class="remark-slide-number">35 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">자바스크립트</h2>
<pre><code class="javascript hljs remark-code"><div class="remark-code-line">>>> [<span class="hljs-string">'10'</span>, <span class="hljs-string">'10'</span>, <span class="hljs-string">'10'</span>].map(<span class="hljs-built_in">parseInt</span>)</div></code></pre>
<pre><code class="javascript hljs remark-code"><div class="remark-code-line">[<span class="hljs-number">10</span>, <span class="hljs-literal">NaN</span>, <span class="hljs-number">2</span>]</div></code></pre><div class="remark-slide-number">35 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><p><img src="./모나드 괴담_files/javascript.jpg" alt="자바스크립트를 쓰기 위해서 자바스크립트를 알아야 할 필요는 없다."><br>
(<a href="https://www.flickr.com/photos/nathansmith/4704268314/in/photostream/">Photo by Nathan Smith</a>. Released under the <a href="https://creativecommons.org/licenses/by/2.0/">Creative Commons Attribution 2.0</a> license.)</p><div class="remark-slide-number">36 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><p><img src="./모나드 괴담_files/javascript.jpg" alt="자바스크립트를 쓰기 위해서 자바스크립트를 알아야 할 필요는 없다."><br>
(<a href="https://www.flickr.com/photos/nathansmith/4704268314/in/photostream/">Photo by Nathan Smith</a>. Released under the <a href="https://creativecommons.org/licenses/by/2.0/">Creative Commons Attribution 2.0</a> license.)</p>
<p>자바스크립트를 쓰기 위해서 자바스크립트를 알아야 할 필요는 없듯이<br>하스켈을 쓰기 위해서 모나드를 알아야 할 필요는 없다</p><div class="remark-slide-number">36 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><h2 id="-do-br-">모든 <code class="remark-inline-code">do</code> 표기법 코드는 모나드로 번역된다.<br>그러니 모나드는 필수 개념이 아닌가?</h2><div class="remark-slide-number">37 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><h2 id="-do-br-">모든 <code class="remark-inline-code">do</code> 표기법 코드는 모나드로 번역된다.<br>그러니 모나드는 필수 개념이 아닌가?</h2>
<p>얼핏 보면, 맞는 말 같지만...</p><div class="remark-slide-number">37 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><h2 id="-c-c-br-c-c-br-">모든 C/C++ 코드는 어셈블리로 번역된다.<br>따라서 C/C++를 배우기 위해서는<br>어셈블리를 먼저 배워야 한다.</h2><div class="remark-slide-number">38 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center hljs-default"><h2 id="-c-c-br-c-c-br-">모든 C/C++ 코드는 어셈블리로 번역된다.<br>따라서 C/C++를 배우기 위해서는<br>어셈블리를 먼저 배워야 한다.</h2>
<p>... 이렇게 바꿔 보면 그렇지만은 않다는 것을 알 수 있다.</p><div class="remark-slide-number">38 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
<li>고양이 두 마리가 있다.</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
<li>고양이 두 마리가 있다.</li>
<li>강아지 두 마리가 있다.</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
<li>고양이 두 마리가 있다.</li>
<li>강아지 두 마리가 있다.</li>
<li>말 두 마리가 있다.</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
<li>고양이 두 마리가 있다.</li>
<li>강아지 두 마리가 있다.</li>
<li>말 두 마리가 있다.</li>
<li>"뭐가 똑같은지 알겠니?"</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<p>(출처: <a href="http://fsharpforfunandprofit.com/posts/why-i-wont-be-writing-a-monad-tutorial/">Why I won't be writing a monad tutorial</a> by scottw.)</p>
<ul>
<li>어린 앨리스는 수학자인 아빠와 함께 동물원에 갔어요.</li>
<li>고양이 두 마리가 있다.</li>
<li>강아지 두 마리가 있다.</li>
<li>말 두 마리가 있다.</li>
<li>"뭐가 똑같은지 알겠니?"</li>
<li>"똑같은 게 없어요!"</li>
</ul><div class="remark-slide-number">39 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<ul>
<li>"아니야, 공통점이 있단다. 뭔지 모르겠니?"</li>
</ul><div class="remark-slide-number">40 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<ul>
<li>"아니야, 공통점이 있단다. 뭔지 모르겠니?"</li>
<li>"다 달라요! 고양이랑 강아지랑 달라요. 고양이랑 말이랑 달라요."</li>
</ul><div class="remark-slide-number">40 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<ul>
<li>"아니야, 공통점이 있단다. 뭔지 모르겠니?"</li>
<li>"다 달라요! 고양이랑 강아지랑 달라요. 고양이랑 말이랑 달라요."</li>
<li>"그럼 이렇게 생각해 보렴. 집합 S는 모든 T ∈ S에 관하여 T ⊂ S이고 S의 원소들의 포함 관계인 ⊂ 는 전순서를 이룬다고 가정하자."</li>
</ul><div class="remark-slide-number">40 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">셈하기</h2>
<ul>
<li>"아니야, 공통점이 있단다. 뭔지 모르겠니?"</li>
<li>"다 달라요! 고양이랑 강아지랑 달라요. 고양이랑 말이랑 달라요."</li>
<li>"그럼 이렇게 생각해 보렴. 집합 S는 모든 T ∈ S에 관하여 T ⊂ S이고 S의 원소들의 포함 관계인 ⊂ 는 전순서를 이룬다고 가정하자."</li>
<li>앨리스는 울음을 터뜨린다.</li>
</ul><div class="remark-slide-number">40 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">과일이란 무엇인가?</h2>
<ul>
<li>과일이 무엇인지 모르는 사람에게 "과일이란 무엇인가?"을 가르칠 때<ul>
<li>사과도 과일이다.</li>
<li>귤도 과일이다.</li>
<li>배도 과일이다.</li>
<li>...</li>
</ul>
</li>
<li>과일이란 식물을 가꾸었을 때 그 식물이 번식의 수단으로서 형성하는, 사람이 먹을 수 있는 열매의 총칭으로서 주로 종자와 과육이 붙어 있는 구조로 이루어져 있으며 대개 수분 과즙이 많고 단맛 또는 신맛이 난다.<ul>
<li>이러지 않습니다.</li>
</ul>
</li>
<li>구체적인 사례로부터 추상적인 개념을 유도하는 것이 우리가 직관적으로 알고 있는 교수법적 상식이다.</li>
</ul><div class="remark-slide-number">41 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">설령 이해하더라도...</h2>
<ul>
<li>모나드라는 개념을 이해하는 것과, 모나드인 타입들(<code class="remark-inline-code">IO</code>, <code class="remark-inline-code">ST</code>, <code class="remark-inline-code">[]</code>, <code class="remark-inline-code">Maybe</code>, ...)을 사용하는 실무적 능력은 별개의 문제다.</li>
<li>범주론에서 말하는 모나드와 하스켈의 모나드는 또 조금씩 다르다.</li>
</ul><div class="remark-slide-number">42 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">설령 이해하더라도...</h2>
<ul>
<li>모나드라는 개념을 이해하는 것과, 모나드인 타입들(<code class="remark-inline-code">IO</code>, <code class="remark-inline-code">ST</code>, <code class="remark-inline-code">[]</code>, <code class="remark-inline-code">Maybe</code>, ...)을 사용하는 실무적 능력은 별개의 문제다.</li>
<li>범주론에서 말하는 모나드와 하스켈의 모나드는 또 조금씩 다르다.</li>
</ul>
<blockquote>
<p>모나드가 무엇인지 이해함으로써 하스켈 프로그래머가 되겠다는 것은 "악기란 무엇인가?"를 이해하면 모든 악기의 연주자가 될 수 있으리라는 믿음과 같다.<br>
Attempting to learn how to use monads by understanding what they are is like asking "What is a musical instrument?" and then assuming once you know the answer to that, you'll be able to play all of the musical instruments.<br>
~kqr, <em><a href="http://two-wrongs.com/the-what-are-monads-fallacy">The "What Are Monads?" Fallacy</a></em> (2015)</p>
</blockquote><div class="remark-slide-number">42 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
<li>어느 순간 모나드가 무엇인지 이해하게 됨</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
<li>어느 순간 모나드가 무엇인지 이해하게 됨</li>
<li>그러자 갑자기 모든 것이 쉽게 느껴짐</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
<li>어느 순간 모나드가 무엇인지 이해하게 됨</li>
<li>그러자 갑자기 모든 것이 쉽게 느껴짐</li>
<li>이 깨달음을 세상에 널리 퍼뜨려 중생을 제도하겠다고 마음먹음</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
<li>어느 순간 모나드가 무엇인지 이해하게 됨</li>
<li>그러자 갑자기 모든 것이 쉽게 느껴짐</li>
<li>이 깨달음을 세상에 널리 퍼뜨려 중생을 제도하겠다고 마음먹음</li>
<li>세상에는 모나드 튜토리얼 하나가 더 추가됨</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">그래서 무슨 일이 생기는가</h2>
<ul>
<li>초보자는 모나드를 반드시 이해해야 한다고 생각함</li>
<li>이해하지 못함 (대개 여기서 포기)</li>
<li>어떻게든 하스켈로 코드를 짜보면서 모나드를 이해해 보려고 애쓴다</li>
<li>어느 순간 모나드가 무엇인지 이해하게 됨</li>
<li>그러자 갑자기 모든 것이 쉽게 느껴짐</li>
<li>이 깨달음을 세상에 널리 퍼뜨려 중생을 제도하겠다고 마음먹음</li>
<li>세상에는 모나드 튜토리얼 하나가 더 추가됨 (이미 셀 수도 없이 많다)</li>
</ul><div class="remark-slide-number">43 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">모나드 튜토리얼</h2><div class="remark-slide-number">44 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">모나드 튜토리얼</h2>
<blockquote>
<p>A 'newbie', in Haskell, is someone who hasn't yet implemented a compiler. They've only written a monad tutorial.<br>
<a href="http://sequence.complete.org/hwn/20061122">Pseudonym</a></p>
</blockquote><div class="remark-slide-number">44 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">모나드 튜토리얼</h2>
<blockquote>
<p>A 'newbie', in Haskell, is someone who hasn't yet implemented a compiler. They've only written a monad tutorial.<br>
<a href="http://sequence.complete.org/hwn/20061122">Pseudonym</a></p>
</blockquote>
<ul>
<li>모나드 튜토리얼을 쓰는 방법에 대한 튜토리얼<ul>
<li>tora, <em><a href="http://www.doc.ic.ac.uk/~tora/monadsI.txt">My how to give a 'monad tutorial' tutorial</a></em> (2010)</li>
<li>Travis Hance, <em><a href="https://tjhance.quora.com/Write-you-a-monad-tutorial">Write you a monad tutorial</a></em> (2014)</li>
</ul>
</li>
</ul><div class="remark-slide-number">44 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">모나드란</h2>
<ul>
<li>모나드는 <strong>타입 클래스</strong>입니다.</li>
<li>타입 클래스는 <strong>타입</strong>의 집합입니다.</li>
<li>타입은 <strong>값</strong>의 집합입니다.</li>
<li>하스켈에서 모나드는 공통점이 있는 여러 개의 타입에 대해서 만들어 놓은 공통의 인터페이스를 말합니다.</li>
<li>따라서, 어떤 타입이 모나드에 속한다고 해도, 다른 모나딕 타입들과는 전혀 상관이 없어 보일 수도 있음.</li>
</ul><div class="remark-slide-number">45 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
<li>하스켈 코드를 많이 작성해 본다. (1천 줄?)</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
<li>하스켈 코드를 많이 작성해 본다. (1천 줄?)</li>
<li>그러다가 어느 순간 이것들이 가지고 있는 공통점에 대해서 알게 된다. (Aha moment)</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
<li>하스켈 코드를 많이 작성해 본다. (1천 줄?)</li>
<li>그러다가 어느 순간 이것들이 가지고 있는 공통점에 대해서 알게 된다. (Aha moment)</li>
<li>하지만 계속 몰라도 별 상관 없다.</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
<li>하스켈 코드를 많이 작성해 본다. (1천 줄?)</li>
<li>그러다가 어느 순간 이것들이 가지고 있는 공통점에 대해서 알게 된다. (Aha moment)</li>
<li>하지만 계속 몰라도 별 상관 없다.</li>
<li><strong>모나드가 무엇인지 따로 배우려고 하지 않는다.</strong></li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">따라서 모나드를 배우기 위해서는</h2>
<ul>
<li>먼저 <code class="remark-inline-code">IO</code> 타입을 써본다.</li>
<li>그리고 <code class="remark-inline-code">Maybe</code> 타입도 써본다.</li>
<li>그리고 리스트 타입도 써본다.</li>
<li>하스켈 코드를 많이 작성해 본다. (1천 줄?)</li>
<li>그러다가 어느 순간 이것들이 가지고 있는 공통점에 대해서 알게 된다. (Aha moment)</li>
<li>하지만 계속 몰라도 별 상관 없다.</li>
<li><strong>모나드가 무엇인지 따로 배우려고 하지 않는다.</strong> 좌절감과 혼란을 초래할 뿐이다.</li>
</ul><div class="remark-slide-number">46 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">"아, 나도 하스켈 하려고 해봤는데, 모나드 때문에..."</h2><div class="remark-slide-number">47 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">이제는 사라져야</h2><div class="remark-slide-number">48 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">"하스켈은 어렵다"</h2>
<p>정확히 말하면,</p>
<blockquote>
<p>다른 언어들(C/C++, 자바, C#, 자바스크립트, 파이선, ...)에 비해 <strong>특별히</strong> 어려운 데가 있을 것이다.</p>
</blockquote><div class="remark-slide-number">49 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">어려움의 종류</h2>
<ul>
<li>배우기 어렵다</li>
<li>쓰기 어렵다</li>
</ul><div class="remark-slide-number">50 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">어려움의 종류</h2>
<ul>
<li>배우기 어렵다</li>
<li>쓰기 어렵다</li>
<li>배우기는 쉬운데 쓰기는 어려운 언어가 있습니다.</li>
</ul><div class="remark-slide-number">50 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">어려움의 종류</h2>
<ul>
<li>배우기 어렵다</li>
<li>쓰기 어렵다</li>
<li>배우기는 쉬운데 쓰기는 어려운 언어가 있습니다. 어셈블리</li>
</ul><div class="remark-slide-number">50 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 "배우기" 어렵다</h2>
<ul>
<li>온갖 음해에 시달렸습니다 여러분.</li>
<li>페다고지, 교수법의 실패</li>
<li>그냥 쓰면 써짐</li>
</ul><div class="remark-slide-number">51 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 "쓰기" 어렵다.</h2>
<ul>
<li>참조 투명성</li>
<li>불변성</li>
<li>재귀</li>
</ul><div class="remark-slide-number">52 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 "쓰기" 어렵다.</h2>
<ul>
<li>참조 투명성</li>
<li>불변성</li>
<li>재귀</li>
</ul>
<p>(어렵다기보다는 불편한 것)</p><div class="remark-slide-number">52 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 "쓰기" 어렵다.</h2>
<ul>
<li>참조 투명성</li>
<li>불변성</li>
<li>재귀</li>
</ul>
<p>(어렵다기보다는 불편한 것)</p>
<ul>
<li>입출력은 쓰기 어려운 것에 속하지 않는다. 쉽다.</li>
</ul><div class="remark-slide-number">52 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">참조 투명성과 불변성</h2>
<ul>
<li>가변 자료를 짓주무르는 방식이 빠른 스크립팅에서 더 편하긴 하다</li>
<li>그러나 stateful한 코드는 코드가 커질수록 치명적인 독이 됨</li>
<li>stateful한 코드는 디버그 하기도 골치아프다.</li>
<li>가변 자료 쓰는 스크립트 언어라도 프로젝트가 되면 MVC 모델 등 state 분리하는 접근이 권장됨</li>
<li>가변 자료를 짓주무르는 코드는 병렬화도 할 수 없다</li>
<li>결국 지향점이 다른 것. 한번 쓰고 버릴 코드라면 가변 자료 쓰는 스크립팅 언어가 더 편하고 빠르고 좋을 것이다</li>
</ul><div class="remark-slide-number">53 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">나는 그래도 가변 자료 하고 싶다!</h2>
<ul>
<li>하스켈에도 가변 자료형 있습니다.</li>
<li><code class="remark-inline-code">ST</code> 액션과 <code class="remark-inline-code">STRef</code>, <code class="remark-inline-code">STArray</code>, <code class="remark-inline-code">STUArray</code> 타입을 쓰시면 됩니다.</li>
</ul><div class="remark-slide-number">54 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">재귀</h2>
<ul>
<li>하스켈 처음 배울 때 제가 가장 헷갈렸던 것</li>
<li>같은 코드에 여러 문맥이 중첩되어 있고, 그게 <code class="remark-inline-code">for</code>와 달리 <code class="remark-inline-code">i</code> 하나만 바뀌는 게 아니다</li>
<li>익숙해지고 나니 전혀 불편하지 않은데, 익숙해지는 비용은 있을 것이다</li>
</ul><div class="remark-slide-number">55 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-for-">재귀가 싫으면 그냥 <code class="remark-inline-code">for</code> 씁시다.</h2>
<ul>
<li>하스켈에도 <code class="remark-inline-code">for</code> 있습니다.</li>
</ul><div class="remark-slide-number">56 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-for-">재귀가 싫으면 그냥 <code class="remark-inline-code">for</code> 씁시다.</h2>
<ul>
<li>하스켈에도 <code class="remark-inline-code">for</code> 있습니다.</li>
</ul>
<pre><code class="haskell hljs remark-code"><div class="remark-code-line"><span class="hljs-keyword">import</span> Control.Monad</div><div class="remark-code-line"></div><div class="remark-code-line"><span class="hljs-title">main</span> :: <span class="hljs-type">IO</span> ()</div><div class="remark-code-line"><span class="hljs-title">main</span> = forM_ [<span class="hljs-number">1</span> .. <span class="hljs-number">10</span>] $ \ i -> <span class="hljs-keyword">do</span></div><div class="remark-code-line">    print i</div></code></pre>
<ul>
<li>코드 생긴 것도 다른 언어의 <code class="remark-inline-code">for</code>와 똑같음.</li>
<li>"이 이상 좋게 해 줄 수 없다."</li>
</ul><div class="remark-slide-number">56 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">하스켈은 수학적인 언어다</h2>
<ul>
<li>왜냐하면 용어가 수학적이고</li>
</ul>
<p><img src="./모나드 괴담_files/Typeclassopedia-diagram.png" alt="Typeclassopedia"></p>
<p>(From <em>Typeclassopedia</em> by Brent Yorgey. Originally published 12 March 2009 in issue 13 of the <em>Monad.Reader</em>)</p>
<ul>
<li>타입 이론 연구 등에 사용되고 있기 때문이다.</li>
</ul><div class="remark-slide-number">57 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
<li>?!</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
<li>?!</li>
<li>하스켈의 공식 목표 중에 "수학적 언어"는 없지만 "애플리케이션 개발에 쓸 수 있는 언어"는 있다</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
<li>?!</li>
<li>하스켈의 공식 목표 중에 "수학적 언어"는 없지만 "애플리케이션 개발에 쓸 수 있는 언어"는 있다</li>
<li>범주론은 초기 하스켈에는 아예 없었다</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
<li>?!</li>
<li>하스켈의 공식 목표 중에 "수학적 언어"는 없지만 "애플리케이션 개발에 쓸 수 있는 언어"는 있다</li>
<li>범주론은 초기 하스켈에는 아예 없었다</li>
<li>하스켈을 "수학적인 언어"라고 부르는 것은 하스켈의 이론적 완성도를 칭송하려는 의도도 있지만, 초보자에게 겁을 주는 역효과도 있다.</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">이것은 마치</h2>
<ul>
<li>수많은 냥짤이 JPEG로 저장되어 있다.</li>
<li>JPEG는 고양이적인 포맷이다.</li>
<li>?!</li>
<li>하스켈의 공식 목표 중에 "수학적 언어"는 없지만 "애플리케이션 개발에 쓸 수 있는 언어"는 있다</li>
<li>범주론은 초기 하스켈에는 아예 없었다</li>
<li>하스켈을 "수학적인 언어"라고 부르는 것은 하스켈의 이론적 완성도를 칭송하려는 의도도 있지만, 초보자에게 겁을 주는 역효과도 있다.</li>
<li>진짜 "수학적인 언어"는 따로 있다. Mathematica, Maple, ...</li>
</ul><div class="remark-slide-number">58 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다<ul>
<li>모나드를 몰라도 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다<ul>
<li>모나드를 몰라도 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈을 배우기 위해서 수학을 잘 해야 되는 것은 아니다</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다<ul>
<li>모나드를 몰라도 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈을 배우기 위해서 수학을 잘 해야 되는 것은 아니다</li>
<li>하스켈 쓰면서 모나드를 모르고 살아도 된다</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다<ul>
<li>모나드를 몰라도 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈을 배우기 위해서 수학을 잘 해야 되는 것은 아니다</li>
<li>하스켈 쓰면서 모나드를 모르고 살아도 된다</li>
<li>"모나드 때문에 하스켈 포기" = "어셈블리 때문에 C 포기"</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-">결론</h2>
<ul>
<li>하스켈 어렵지 않다.</li>
<li>하스켈은 다른 프로그래밍 언어와 그렇게 극단적으로 다르지 않다. (일부러 비슷해 보이기 위한 노력까지 했다)</li>
<li>모나드를 몰라도 하스켈을 쓸 수 있다<ul>
<li>모나드를 몰라도 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈을 배우기 위해서 수학을 잘 해야 되는 것은 아니다</li>
<li>하스켈 쓰면서 모나드를 모르고 살아도 된다</li>
<li>"모나드 때문에 하스켈 포기" = "어셈블리 때문에 C 포기"</li>
<li>더 이상 이런 불행이 없었으면.</li>
</ul><div class="remark-slide-number">59 / 60</div></div></div></div><div class="remark-slide-notes"></div></div><div class="remark-slide-container"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content center middle hljs-default"><h2 id="-">감사합니다.</h2><div class="remark-slide-number">60 / 60</div></div></div></div><div class="remark-slide-notes"></div></div></div>
<div class="remark-preview-area"><div class="remark-slide-container remark-fading"><div class="remark-slide-scaler" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;"><div class="remark-slide"><div class="remark-slide-content hljs-default"><h2 id="-del-del-"><del>온갖 음해에 시달렸습니다</del></h2>
<ul>
<li>하스켈은 어렵다</li>
<li>모나드가 어려워서 하스켈은 어렵다</li>
<li>모나드를 알아야 하스켈을 쓸 수 있다<ul>
<li>모나드를 알아야 <em>실용적</em> 하스켈을 쓸 수 있다</li>
</ul>
</li>
<li>하스켈은 수학적인 언어다</li>
<li>아무튼 모나드를 배워야 한다</li>
</ul><div class="remark-slide-number">2 / 60</div></div></div></div><div class="remark-slide-notes"></div></div></div>
<div class="remark-backdrop"></div>
<div class="remark-pause" style="transform: scale(1.17474); left: 13.7805px; top: 0px;">
  <div class="remark-pause-lozenge">
    <span>Paused</span>
  </div>
</div>
<div class="remark-help" style="width: 1210px; height: 681px; transform: scale(1.17474); left: 13.7805px; top: 0px;">
  <div class="remark-help-content">
    <h1>Help</h1>
    <p><b>Keyboard shortcuts</b></p>
    <table class="light-keys">
      <tbody><tr>
        <td>
          <span class="key"><b>↑</b></span>,
          <span class="key"><b>←</b></span>,
          <span class="key">Pg Up</span>,
          <span class="key">k</span>
        </td>
        <td>Go to previous slide</td>
      </tr>
      <tr>
        <td>
          <span class="key"><b>↓</b></span>,
          <span class="key"><b>→</b></span>,
          <span class="key">Pg Dn</span>,
          <span class="key">Space</span>,
          <span class="key">j</span>
        </td>
        <td>Go to next slide</td>
      </tr>
      <tr>
        <td>
          <span class="key">Home</span>
        </td>
        <td>Go to first slide</td>
      </tr>
      <tr>
        <td>
          <span class="key">End</span>
        </td>
        <td>Go to last slide</td>
      </tr>
      <tr>
        <td>
          Number + <span class="key">Return</span>
        </td>
        <td>Go to specific slide</td>
      </tr>
      <tr>
        <td>
          <span class="key">b</span>&nbsp;/
          <span class="key">m</span>&nbsp;/
          <span class="key">f</span>
        </td>
        <td>Toggle blackout / mirrored / fullscreen mode</td>
      </tr>
      <tr>
        <td>
          <span class="key">c</span>
        </td>
        <td>Clone slideshow</td>
      </tr>
      <tr>
        <td>
          <span class="key">p</span>
        </td>
        <td>Toggle presenter mode</td>
      </tr>
      <tr>
        <td>
          <span class="key">t</span>
        </td>
        <td>Restart the presentation timer</td>
      </tr>
      <tr>
        <td>
          <span class="key">?</span>,
          <span class="key">h</span>
        </td>
        <td>Toggle this help</td>
      </tr>
    </tbody></table>
  </div>
  <div class="content dismiss">
    <table class="light-keys">
      <tbody><tr>
        <td>
          <span class="key">Esc</span>
        </td>
        <td>Back to slideshow</td>
      </tr>
    </tbody></table>
  </div>
</div>



</body></html>
