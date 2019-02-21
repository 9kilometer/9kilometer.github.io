---
title: "Hello World!"
excerpt: "첫 블로그, 첫 글!"
header: 
    overlay_image: /assets/resources/post_header.jpg
last_modified_at: 2019-02-21T23:00:00
category: record
tag: 
    - jekyll
    - 기록
toc: true
---


[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 테마를 적용한 블로그를 만들었다!  
맘에 드는 테마가 이 테마 외에도 몇 개 있었는데, 카테고리/태그 별로 보기와 검색 기능이 기본적으로 들어가있어 결국엔 이 테마를 선택했다. 가장 외형이 맘에 드는 테마를 기반으로 원하는 기능만 직접 추가할 수 있다면 좋겠지만, 이쪽 지식이 짧아서 어쩔 수 없었다...  

어쨋든, 이 글은 작성한 마크다운이 해당 테마에서 어떻게 보일 지 확인하기 위한 글이다.  

---
<strong>데모 사이트의 글 `Markup: HTML Tags and Formatting`에서 가져옴.</strong>  
[원본 주소](https://mmistakes.github.io/minimal-mistakes/markup/markup-html-tags-and-formatting/#definition-lists)

---
A variety of common markup showing how the theme styles them.

## Header two

### Header three

#### Header four

##### Header five

###### Header six

## Blockquotes

Single line blockquote:

> Stay hungry. Stay foolish.

Multi line blockquote with a cite reference:

> People think focus means saying yes to the thing you've got to focus on. But that's not what it means at all. It means saying no to the hundred other good ideas that there are. You have to pick carefully. I'm actually as proud of the things we haven't done as the things I have done. Innovation is saying no to 1,000 things.

<cite>Steve Jobs</cite> --- Apple Worldwide Developers' Conference, 1997
{: .small}

## Tables

| Employee         | Salary |                                                              |
| --------         | ------ | ------------------------------------------------------------ |
| [John Doe](#)    | $1     | Because that's all Steve Jobs needed for a salary.           |
| [Jane Doe](#)    | $100K  | For all the blogging she does.                               |
| [Fred Bloggs](#) | $100M  | Pictures are worth a thousand words, right? So Jane × 1,000. |
| [Jane Bloggs](#) | $100B  | With hair like that?! Enough said.                           |

| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|-----------------------------|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=============================|
| Foot1   | Foot2   | Foot3   |

## Definition Lists

Definition List Title
:   Definition list division.

Startup
:   A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.

#dowork
:   Coined by Rob Dyrdek and his personal body guard Christopher "Big Black" Boykins, "Do Work" works as a self motivator, to motivating your friends.

Do It Live
:   I'll let Bill O'Reilly [explain](https://www.youtube.com/watch?v=O_HyZ5aW76c "We'll Do It Live") this one.

## Unordered Lists (Nested)

  * List item one 
      * List item one 
          * List item one
          * List item two
          * List item three
          * List item four
      * List item two
      * List item three
      * List item four
  * List item two
  * List item three
  * List item four

## Ordered List (Nested)

  1. List item one 
      1. List item one 
          1. List item one
          2. List item two
          3. List item three
          4. List item four
      2. List item two
      3. List item three
      4. List item four
  2. List item two
  3. List item three
  4. List item four

## Forms

<form>
  <fieldset>
    <legend>Personalia:</legend>
    Name: <input type="text" size="30"><br>
    Email: <input type="text" size="30"><br>
    Date of birth: <input type="text" size="10">
  </fieldset>
</form>

## Buttons

Make any link standout more when applying the `.btn` class.

```html
<a href="#" class="btn--success">Success Button</a>
```

[Default Button](#){: .btn}
[Primary Button](#){: .btn .btn--primary}
[Success Button](#){: .btn .btn--success}
[Warning Button](#){: .btn .btn--warning}
[Danger Button](#){: .btn .btn--danger}
[Info Button](#){: .btn .btn--info}
[Inverse Button](#){: .btn .btn--inverse}
[Light Outline Button](#){: .btn .btn--light-outline}

```markdown
[Default Button Text](#link){: .btn}
[Primary Button Text](#link){: .btn .btn--primary}
[Success Button Text](#link){: .btn .btn--success}
[Warning Button Text](#link){: .btn .btn--warning}
[Danger Button Text](#link){: .btn .btn--danger}
[Info Button Text](#link){: .btn .btn--info}
[Inverse Button](#link){: .btn .btn--inverse}
[Light Outline Button](#link){: .btn .btn--light-outline}
```

[X-Large Button](#){: .btn .btn--primary .btn--x-large}
[Large Button](#){: .btn .btn--primary .btn--large}
[Default Button](#){: .btn .btn--primary }
[Small Button](#){: .btn .btn--primary .btn--small}

```markdown
[X-Large Button](#link){: .btn .btn--primary .btn--x-large}
[Large Button](#link){: .btn .btn--primary .btn--large}
[Default Button](#link){: .btn .btn--primary }
[Small Button](#link){: .btn .btn--primary .btn--small}
```

## Notices

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice}` class.
{: .notice}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--primary}` class.
{: .notice--primary}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--info}` class.
{: .notice--info}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--warning}` class.
{: .notice--warning}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--success}` class.
{: .notice--success}

**Watch out!** This paragraph of text has been [emphasized](#) with the `{: .notice--danger}` class.
{: .notice--danger}

## HTML Tags

### Address Tag

<address>
  1 Infinite Loop<br /> Cupertino, CA 95014<br /> United States
</address>

### Anchor Tag (aka. Link)

This is an example of a [link](http://apple.com "Apple").

### Abbreviation Tag

The abbreviation CSS stands for "Cascading Style Sheets".

*[CSS]: Cascading Style Sheets

### Cite Tag

"Code is poetry." ---<cite>Automattic</cite>

### Code Tag

You will learn later on in these tests that `word-wrap: break-word;` will be your best friend.

### Strike Tag

This tag will let you <strike>strikeout text</strike>.

### Emphasize Tag

The emphasize tag should _italicize_ text.

### Insert Tag

This tag should denote <ins>inserted</ins> text.

### Keyboard Tag

This scarcely known tag emulates <kbd>keyboard text</kbd>, which is usually styled like the `<code>` tag.

### Preformatted Tag

This tag styles large blocks of code.

<pre>
.post-title {
	margin: 0 0 5px;
	font-weight: bold;
	font-size: 38px;
	line-height: 1.2;
	and here's a line of some really, really, really, really long text, just to see how the PRE tag handles it and to find out how it overflows;
}
</pre>

### Quote Tag

<q>Developers, developers, developers&#8230;</q> &#8211;Steve Ballmer

### Strong Tag

This tag shows **bold text**.

### Subscript Tag

Getting our science styling on with H<sub>2</sub>O, which should push the "2" down.

### Superscript Tag

Still sticking with science and Albert Einstein's E = MC<sup>2</sup>, which should lift the 2 up.

### Variable Tag

This allows you to denote <var>variables</var>.

---

<h3>그 외 기록 - 폰트 설정</h3>
<h4>폰트 추가 & 변경</h4>
```scss
/* font-face 추가 */
@font-face {
   font-family: "myFont";
   src: url("/assets/fonts/myFont.ttf") format('truetype');
}
$myFont: "myFont";
/* css import */
@import "/assets/fonts/kopub/css/myFont2.css";
$myFont2: "myFont2", sans-serif !default;
```

<h4>폰트 크기</h4>  
포스트 제목이나 본문 제목(`h1`~`h6`), 인용구, 코드 블럭 등의 글자 크기는 `_variables.scss`에서 설정된 `$type-size-[1-8]`을 사용한다. 글자 크기를 변경하길 원하는 부분이 어떤 변수를 가져다 쓰는 지 확인하고 해당 변수의 값을 수정하거나, `_base.scss`에서 직접 원하는 값을 넣어주자.  
**_variables.scss**
```scss
  /* type scale */
  $type-size-1: 2.441em !default; // ~39.056px  
  $type-size-2: 1.953em !default; // ~31.248px
  $type-size-3: 1.563em !default; // ~25.008px  
  $type-size-4: 1.25em !default; // ~20px  
  $type-size-5: 1em !default; // ~16px  
  $type-size-6: 0.75em !default; // ~12px 
  $type-size-7: 0.6875em !default; // ~11px
  $type-size-8: 0.625em !default; // ~10px
  ```
**_base.scss**
```scss
  h1 {
  margin-top: 0;
  font-size: $type-size-3; // 이 부분 변경
  }

  h2 {
  font-size: $type-size-4;
  }
```
