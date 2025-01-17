# 다양한 종류의 카테고리
원본 사이트: [Categories Great and Small](https://bartoszmilewski.com/2014/12/05/categories-great-and-small/)

---

> 이 글은 프로그래머를 위한 카테고리 이론이라는 책의 일부입니다. 이전 글은 [타입과 함수](/contents/part1/types-and-functions.md) 입니다. 목차는 [여기서](/README.md) 확인하실 수 있습니다.

이 글을 통해 다양한 예시를 공부하고나면 카테고리에 감사하게 될지도 모릅니다. 카테고리는 그 형태와 크기가 무궁무진하며 때론 생각지도 못 한 곳에서 튀어나오기도 합니다. 아주 간단한 것부터 시작해보겠습니다.

## No Objects

최고로 작은 카테고리는 객체와 사상(morphism)이 모두 존재하지 않는 카테고리입니다. 그 존재 자체는 슬플지도 모르지만 다른 카테고리(예를 들어, 모든 것을 포함하는 카테고리)의 맥락에선 중요한 역할을 합니다. 공집합이 말이 된다 생각하신다면 빈 카테고리도 생각하실 수 있으시겠죠?

## Simple Graphs

우리는 두 객체를 화살표로 이어주는 것만으로 카테고리를 만들 수 있습니다. 그러면 하나의 방향을 가진 화살표로 시작해서 몇 개의 화살표로 이루어진 간단한 카테고리를 생각해보겠습니다. 먼저 각 노드에게 자기 자신으로 향하는 화살표를 추가해줍니다. 그리고 하나의 끝이 다른 하나의 시작을 가리키는 두 화살표를 찾습니다. (다른 말로, 합성가능한 두 개의 화살표) 이 두 화살표를 하나의 화살표로 만들어서 합성을 표시합니다. 새로운 화살표를 추가할 때마다 다른 화살표와 자기 자신의 합성을 항상 고려해야 합니다. (자기 자신을 가리키는 화살표는 제외합니다) 계속 하다보면 무한대의 화살표를 만들게 되겠지만 괜찮습니다.

이러한 과정을 다른 시각으로 보면 여러분은 그래프의 모든 노드를 객체로 가지는 카테고리를 만들고 있었고 모든 합성 가능함을 나타내는 그래프의 변은 사상이라고 볼 수 있습니다. (자기 자신을 가리키는 화살표 또한 길이가 0인 특별한 경우의 사상으로 볼 수 있습니다)

이러한 카테고리를 주어진 그래프에서 생성된 자유(free) 카테고리라고 합니다. 이와 관련된 내용은 나중에 더 자세히 알아보도록 하겠습니다.

## Orders

이제 완전히 다른 카테고리를 알아봅시다! 카테고리의 사상이 두 객체의 관계를 나타내고 이 관계가 작거나 같음을 나타낸다고 합니다. 이게 진짜 카테고리인지 알아보겠습니다. 자기 자신에 대한 사상이 올바를까요? 네, 모든 객체는 자기 자신보다 작거나 같죠! 합성이 가능한가요? a <= b 이고 b <= c 라면 a <= c이니 가능합니다! 이 합성이 결합 법칙을 지키나요? 네! 이러한 관계를 가지는 카테고리를 preorder라고 부릅니다. preorder도 물론 카테고리입니다.

조금 더 강한 관계를 만들어보겠습니다. a <= b 이면서 b <= a 인 경우가 있다면 a는 분명 b와 같을 수 밖에 없을 것입니다. 이러한 카테고리를 partial order라고 부릅니다.

마지막으로 두 객체가 서로, 한 방향 또는 반대 방향의 관계를 가진다면 이를 linear order 또는 total order라고 부릅니다.

앞에 나온 order 집합들을 카테고리로 나타내보겠습니다. preorder는 어떤 객체 a에서 어떤 객체 b로 가는 사상이 많아 봐야 하나인 카테고리입니다. 이러한 카테고리를 "thin"이라고 부르기도 합니다. preorder는 thin category입니다.

카테고리 C의 객체 a에서 객체 b로 가는 사상의 집합을 hom-set이라고 하며, C(a, b)(또는 HomC(a, b))라고 적습니다. 그러니 preorder의 모든 hom-set은 비었거나 싱글톤입니다. 여기엔 a에서 a로 가는 사상의 집합이고 반드시 싱글톤인 hom-set C(a, a)도 포함합니다. preorder에선 순환이 생길 수도 있는데, 순환은 partial order에선 금지되어 있습니다.

정렬때문에 preorder인지 partial order인지 그리고 total order인지 알아내는 것은 아주 중요한 문제입니다. 퀵정렬, 버블 정렬, 머지 정렬 등의 정렬 알고리즘은 total order에서만 제대로 작동하기 때문입니다. Partial order의 정렬은 topological 정렬을 사용해야 합니다.

## Monoid as Set

모노이드(Monoid)는 당황스러울 정도로 간단하지만 놀랍도록 강력한 개념입니다. 모노이드는 기초 산수의 더하기 곱하기 개념을 바탕으로 합니다. 모노이드는 프로그래밍에선 아주 흔한 개념입니다. 예를 들면 스트링, 리스트, fold가 가능한 데이터 구조, concurrent 프로그래밍의 future, 함수형 반응형 프로그래밍의 event 등이 있습니다.

전통적으로 모노이드는 두 가지 연산을 원소로 하는 집합으로 정의되어 왔습니다. 이 연산은 결합성을 필수로 가지며 unit과 같은 특별한 하나의 원소가 존재합니다.

자연수와 0을 모노이드의 예로 들어보겠습니다.
결합성을 가진다는 것은 다음과 같은 작업이 가능하다는 뜻입니다.

```
(a + b) + c = a + (b + c)
```
(다른 말로는 숫자를 더할 땐 괄호를 생략할 수 있다는 뜻이죠.)

중립 요소는 0인데 왜냐하면 다음 두 식을 예로 들 수 있습니다.

```
0 + a = a
```

```
a + 0 = a
```

두 번째 식은 불필요한데 왜냐하면 덧셈은 교환 법칙이 성립하지만 교환 법칙은 모노이드의 정의에 포함되지 않기 때문입니다. 예를 들어 연속된 스트링의 경우는 교환 법칙이 성립하지 않지만 모노이드이기 때문입니다. 여기서 모노이드 중립 요소는 빈 스트링이며 양쪽을 바꾸지 않고 왼쪽과 오른쪽 모두 붙을 수 있기 때문입니다.

하스켈에선 모노이드를 위한 타입 클래스를 정의할 수 있는데 중립 요소는 `mempty`, 이진 연산은 `mappend`라고 부르겠습니다.

```
class Monoid m where
    mempty  :: m
    mappend :: m -> m -> m
```

두 개의 인자를 받는 함수라는 의미의 타입 서명인 `m->m->m`은 처음 보기엔 낯설 수 있지만 커링에 대해 얘기하고 나면 완벽하게 이해하실 것입니다. 여러분은 다음과 같은 두 가지 방식으로 이해하셨을 것입니다. 하나는 여러 개의 인자를 받는 함수가 있고 가장 오른쪽이 반환하는 타입인 것과 다른 하나는 가장 왼쪽을 받아서 함수를 반환하는 것입니다. 후자의 방식은 `m->(m->m)` 이렇게 괄호를 추가하는 것으로 강조할 수 있을 것입니다. (화살표는 오른쪽 연산이 우선순위가 높기 때문에 의미없긴 합니다.) 이러한 해석 방식은 나중에 알아보도록 하겠습니다.

하스켈에는 `mempty`와 `mappend`를 모노이드스러운 방식으로 표현할 수 있는 방법이 존재하지 않습니다. 이를 만족시키는 것은 프로그래머에게 주어진 책임입니다.

하스켈 클래스는 C++의 클래스처럼 거슬리지 않습니다. 여러분이 새로운 타입을 정의하려고 할 때 이전 클래스를 구체적으로 적을 필요가 없다는 뜻입니다. 이는 미뤄도 되며 주어진 타입이 어떤 클래스의 인스턴스가 되는 것은 더 늦게 해도 됩니다. 예를 들어 `String`이 `mempty`와 `mappend`의 구현을 제공해서 모노이드가 되었다고 해보겠습니다. (보통의 시나리오에선 이미 구현되어 있습니다)

```
instance Monoid String where
    mempty = ""
    mappend = (++)
```

`mappend`를 보면 리스트를 이어주는 연산자인 `(++)`를 재사용했는데, `String`은 그저 문자의 목록이기 때문에 그렇습니다.

하스켈 문법에 대한 설명: 어떤 infix 연산자는 괄호로 둘러싸이면 두 개의 인자를 받는 함수로 변환할 수 있습니다. 두 스트링을 `++` 로 합치는 연산은 다음과 같이 작동합니다.

```
"Hello " ++ "world!"
```

또는 `(++)`에 두 개의 인자를 넘기는 방식으로 코드를 작성할 수도 있습니다.

```
(++) "Hello " "world!"
```

함수에 인자를 넘기는 방식에 어떠한 쉼표나 괄호를 사용하지 않았다는 사실을 기억하세요. (이 점이 하스켈을 배우면서 가장 익숙해지기 어려운 부분 중 하나일 것입니다.)

하스켈이 제공하는 두 함수의 동등함을 표현하는 방식을 강조할만한 가치가 있습니다.

```
mappend = (++)
```

이것은 아래와 같은 함수가 만들어낸 값을 비교하는 것과는 개념적으로 다릅니다.

```
mappend s1 s2 = (++) s1 s2
```

전자는 **Hask** 카테고리의 사상의 동등함을 비교하는 내용입니다. 이러한 등식은 간결할 뿐만 아니라 다른 카테고리에도 적용할 수 있습니다. 후자는 extensional equality라고 부르며 어떠한 두 입력값에 대하여 `mappend`의 출력과 `(++)`의 출력이 같다는 것을 의미합니다. 인자의 값은 종종 포인트(포인트 x에 대한 f의 값)를 호출하기 때문에 이를 point-wise equality라고도 부릅니다. 인자를 지정하지 않고 함수의 동등 비교하는 것은 *point-free* 라고 부릅니다. (우연히도 point-free 등식은 종종 포인트에 의해 상징화된 함수의 합성을 수반하기 때문에 초심자에겐 혼돈을 줄 수 있습니다.)

C++에서 모노이드를 선언하는 것에 제일 가까운 방식은 제안된 문법을 사용하는 것입니다.

```
template<class T>
  T mempty = delete;

template<class T>
  T mappend(T, T) = delete;

template<class M>
  concept bool Monoid = requires (M m) {
    { mempty<M> } -> M;
    { mappend(m, m); } -> M;
  };
```

첫 번째 정의에선 template 값을 사용합니다. 이것과 동형인 값은 값의 가족들입니다. 각 타입의 다른 값들이죠.

`delete`라는 키워드는 기본 값이 정의되지 않았다는 것을 의미합니다. 이는 모든 경우에 대해 각각 명세해야 합니다. `mappend`도 동일하게 기본 값이 존재하지 않습니다.

`Monoid`라는 개념은 주어진 타입 M에 대하여 `mempty`와 `mappend`이 적절하게 정의되어서 존재하는지 테스트하는 predicate입니다.

모노이드 개념의 실현은 적절한 구현을 통해 만들어낼 수 있습니다.

```
template<>
std::string mempty<std::string> = {""};

std::string mappend(std::string s1, std::string s2) {
    return s1 + s2;
}
```

## Monoid as Category

앞에서는 집합의 요소의 측면에서 모노이드의 정의에 대해 알아보았습니다. 아시다시피, 카테고리 이론에서는 집합과 요소를 떠나서 객체와 사상에 대해 얘기해야 하지 않을까요? 그러니 이제 시각을 약간 돌려서 다시 모노이드를 카테고리 측면에서 바라보도록 하겠습니다.

예를 들어 모든 자연수에 5를 더하는 연산이 있다고 치겠습니다. 이 연산은 0을 5로, 1을 6으로, 2를 7로 만들 것입니다. 이는 자연수 집합에 정의된 함수입니다. 이젠 함수와 집합을 얻었네요 좋습니다. 일반적으론 어떤 숫자 n에 대해 n을 더하는 함수인 n의 "adder"가 있습니다.

그렇다면 adder는 어떻게 합성할까요? 5를 더하는 함수와 7을 더하는 함수를 합성하면 12를 더하는 함수가 될 것입니다. 그러니 adder 함수의 합성은 덧셈의 규칙을 유지합니다. 덧셈을 함수 합성으로 대체할 수 있겠네요. 이것 또한 좋습니다.

잠시만요, 한 가지 더 있습니다. 중립 요소인 0에 대한 adder도 존재합니다. 0을 더해도 무언가 바뀌지 않으니 0을 더하는 것은 자연수의 자기 자신을 표현하는 함수라고 생각할 수 있겠습니다.

전통적인 덧셈 규칙을 제공하는 대신에 이제 저는 여러분에게 adder를 합성하는 규칙을 어떠한 정보의 손실 없이 드리겠습니다. adder의 합성은 결합 법칙이 성립한다는 사실을 기억해주세요. 왜냐하면 함수의 합성은 결합 법칙을 지키기 때문입니다. 그리고 자기 자신을 나타내는 함수는 zero adder가 있습니다.

눈치가 빠른 독자라면 정수를 adder로 맵핑하는 것이 앞에서 알아봤던 `mappend` 타입 서명인 `m->(m->m)`의 두 번째 해석 방법이라는 것을 아셨을 것입니다. 이는 `mappend`가 모노이드 집합의 요소를 그 집합에서 활동하는 함수에 맵핑하는 것을 의미합니다.

지금부터는 자연수 집합에 대해서 잊고 하나의 객체만 생각해주셨으면 합니다. 다양한 사상을 가지는 adder입니다. 모노이드는 하나의 객체를 가지는 카테고리입니다. 실제로도 monoid란 이름은 그리스어로 single을 의미하는 *mono* 에서 따왔습니다. 모든 모노이드는 합성의 규칙을 따르는 사상의 집합을 가지는 하나의 객체 카테고리로 설명할 수 있습니다.

<p align="center">
	<img src="/img/img_part1-3_1.jpg" width="238" />
</p>

연속된 스트링은 흥미로운 케이스입니다. 왜냐하면 왼쪽에도 붙일 수 있고 오른쪽에도 붙일 수 있기 때문입니다. 두 모델의 합성 테이블은 거울에 비친듯이 반대입니다. "foo" 뒤에 "bar"를 붙이는 것과 "bar"에 "foo"를 접두어로 붙이는 것이 같다는 것을 보면 쉽게 이해할 수 있을 것입니다.

이런 질문이 생겼을 수 있습니다. "하나의 객체를 가지는 카테고리인 모든 모노이드가 고유한 바이너리 연산자 모노이드를 정의할까?" 이를 다르게 말하면 하나의 객체를 가지는 카테고리에서는 언제나 집합을 추출해낼 수 있다는 의미입니다. 이 집합은 사상의 집합입니다. 우리 예시에선 adder들이겠죠. 이 집합에서 이진 연산을 쉽게 정의할 수 있습니다. 집합의 요소 둘을 모노이드 곱(product)을 하는 것은 이에 맞는 사상을 합성하는 것과 같다는 것입니다. 만약 M(m, m)의 두 요소를 `f`와 `g`로 준다면 그들의 곱은 `g∘f` 합성에 대응한다는 의미입니다. 이러한 사상들의 원본과 목표가 같은 객체이기 때문에 그 합성은 언제나 존재합니다. 그리고 카테고리의 규칙에 의해 결합 법칙도 성립합니다. 자기 자신을 가리키는 사상도 중립 요소의 곱이라고 생각하시면 됩니다. 그러니 카테고리 모노이드는 항상 집합 모노이드로 설명할 수 있습니다. 결과적으로 그들은 하나이며 동일합니다.

<p align="center">
	<img src="/img/img_part1-3_2.jpg" width="300" />
	<p>모노이드 hom-set은 집합의 한 요소와 그것의 사상이라고 볼 수 있습니다.</p>
</p>

수학자들에겐 사상은 집합을 이룰 필요가 없다는 내용이 있습니다. 카테고리의 세계에는 집합보다 더 큰 것들도 존재합니다. 집합을 형성하는 두 객체 사이의 사상을 의미하는 카테고리는 small이라고 부릅니다. 약속드렸듯이 저는 대부분의 미묘한 내용들은 무시할 것이지만 여기선 기록을 위해 언급해야 할 것 같습니다.

카테고리 이론의 아주 많은 흥미로운 현상들은 hom-set의 요소들이 합성의 규칙을 따르는 합성도 될 수 있고 집합의 포인트가 될 수도 있다는 사실에 근간을 두고 있습니다. M의 사상의 합성은 집합 M(m, m)의 모노이드 곱으로 해석될 수 있습니다.

## 도움주신 분

C++ 모노이드 개념 코드를 새롭게 써준 Andrew Sutton에게 감사드리고 그와 Bjarne Stroustrup의 최신 제안이 없었다면 새로 쓸 수도 없었을 것입니다.

다음: [Kleisli 카테고리](/contents/part1/kleisli-category.md)를 이용해 로깅하는 순수 함수 프로그래밍하기

---

공부 목적으로 번역을 하고 있습니다! 잘못된 점에 대한 이슈나 PR은 언제든지 환영합니다 :)
