---
layout: default
title: Markdown
nav_order: 1
permalink: docs/Markdown
---

# <b>Markdown</b>
{: .no_toc }

블로그를 시작하면서 필요한 markdown 문법을 간단히 정리해보았습니다<br>
추후 다른 기능이 필요하면 해당 기능에 대해 찾아서 내용을 추가할 예정입니다

## Text

*Italic* \ **Bold** \ ***Bold Italic*** \
<kbd>keyboard tag</kbd> \
`inline code`
~~strikethrough~~
# Header1


### Code

```html
*Italic* \ **Bold** \ ***Bold Italic*** \
<kbd>keyboard tag</kbd> \
`inline code`
~~strikethrough~~
# Header1 <!-- Header2 is ## Header2 ~ Header6 is ###### Header6 -->
```

---

## Link

[internal link](#internal-link)

[internal link 2](#internal-link2)

footnote[^footnote], another footnote[^fn2]

[This Page](/docs/Markdown)

<https://prhymery.github.io/docs/Markdown>

[^footnote]: The footnote source
[^fn2]: The 2nd footnote source

### internal link

###### Internal-link2

### Code

```html
[internal link](#internal-link)

[internal link 2](#internal-link2)

footnote[^footnote], another footnote[^fn2]

[This Page](/docs/Markdown)

<https://prhymery.github.io/docs/Markdown>

[^footnote]: The footnote source
[^fn2]: The 2nd footnote source

### internal link

###### Internal-link2

```

---

## Paragraph

#### Line break

- List
    + List in List
        * List in List
        * [ ] To do
        * [x] To do

1. 1
2. 2
   1. 2-1E
   - [ ] To do

#### Description

: This is Description
: This is Description about Description

#### Toggle

<details open><summary>opened toggle</summary><div markdown="1">
 1. [Markdown](https://prhymery.github.io/docs/Markdown) <br>
toggle end
  </div></details>

<details close><summary>closed toggle</summary><div markdown="1">
 1. [Markdown](https://prhymery.github.io/docs/Markdown) <br>
toggle end
  </div></details>

### Code

```html
#### Line break
- List
    + List in List
        * List in List
        * [ ] To do
        * [x] To do

1. 1
2. 2
   1. 2-1E
   - [ ] To do

#### Description
: This is Description
: This is Description about Description

#### Toggle

<details open><summary>opened toggle</summary><div markdown="1">
 1. [Markdown](https://prhymery.github.io/docs/Markdown) <br>
toggle end
  </div></details>

<details close><summary>closed toggle</summary><div markdown="1">
 1. [Markdown](https://prhymery.github.io/docs/Markdown) <br>
toggle end
  </div></details>
```

---

## Block

```
Code block
```
> Blockquotes
>> Blockquotes in blockquotes

> tip
{: .prompt-tip }

> info
{: .prompt-info }

> warning
{: .prompt-warning }

> danger
{: .prompt-danger }

---

#### Table

|table|C+|C#|
|:-|:-:|-:|
|Left alingned|center alingned|right alingned|
|pointer|o|x|

### Code

```html
\```<!-- Code block start(w/o \ , just ```) -->
Code block
\```<!-- Code block end(w/o \ , just ```) -->

> Blockquotes
>> Blockquotes in Blockquotes

> tip
{: .prompt-tip }

> info
{: .prompt-info }

> warning
{: .prompt-warning }

> danger
{: .prompt-danger }

--- <!-- Underline -->

|table|C+|C#|
|:-|:-:|-:|
|Left alingned|center alingned|right alingned|
|pointer|o|x|
```

---

## Image

![img-description](/assets/images/DotNET/UnityAPICompatibilityLevel.png)
_Unity/Project Settings/Player/API Compatibility Level_
{: .text-center }

### Code

```html
![img-description](/assets/images/DotNET/UnityAPICompatibilityLevel.png)
_Unity/Project Settings/Player/API Compatibility Level_
{: .text-center }   // 가운데 정렬
```

---

## ETC

file path `/path/to/the/file.extend`{: .filepath}.


### Code

```html
file path `/path/to/the/file.extend`{: .filepath}.
```
