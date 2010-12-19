# 
# Program:              $RCSfile: README-CX-model.ja,v $  $Revision: 60.6 $
# 
# Purpose:              README of CX-model (Japanese)
# 
# Author:               N.Atsumi  2006/02/04
#                       S.Yamamoto  2006/02/04
#                       N.Uehara  2009/10/08
#                       E.Hirumuta  2009/10/10
# 
# Copyright:            N.Atsumi  2006
#                       This file is a product of the project Sapid.
#

# 
# $Id: README-CX-model.ja,v 60.6 2010/04/11 23:50:32 yamamoto Exp yamamoto $
# 

目次:

	1 はじめに
	2 使用方法
	3 CX-model
	3.1 CX-modelの要素
	3.2 属性一覧
	3.3 flow 要素
	4 問題

==============================

1 はじめに

spdMkCXModelはCX-modelに基づいたXML形式のリポジトリを生成するコマンドで
ある．

注意: CX-modelは開発中であり，モデル要素，属性が変更・追加される可能性が
ある．また，spdMkCXModelは一部のモデル要素に対してoffsetがずれる．

------------------------------

2 使用方法
% spdMkCXModel [options] [target_program]

-d オプションを指定しない場合，SDBが構築されているディレクトリで実行す
る必要がある．出力ファイル名はデフォルトでは <fileId>.xml であり，-sdbD
オプションを指定した場合は <ソースファイル名>.xml である．

オプションを以下に示す．
-d directory    : SDBディレクトリの位置を指定する．デフォルトでは"SDB"
である．
-f              : フロー情報を付加する．
-h              : ヘルプを表示する．
-sdbD directory : XMLファイルの出力先を指定する．
-t              : 型情報を付加する．
-v              : 詳細メッセージを表示する．
-w              : 警告メッセージを表示する．
-D directory    : 仕様ファイルの出力先を指定する．デフォルトでは"SPEC"
である．
-P              : 作業ファイルを保存する．
-S directory    : インクルードディレクトリを指定する．
target_program  : ターゲットプログラムを指定する．デフォルトでは"a.out"
である．

型情報を付加する場合，spdMkCXModelはサブコマンドspdMkCXTypeInfosを実行
する．spdMkCXTypeInfosは型情報を<ターゲットプログラム名>_typeInfos.xml
に出力し，これを中間形式として再度読み込み，spdMkCXModelが出力したCX-
model文書に挿入する．

------------------------------

3 CX-model

3.1 CX-modelの要素

CX	     : 型情報を付加した場合の CX-model XML 文書のルートノード
	       型情報を付加しない場合，この要素は出力されない．
	       Child nodes:
	       (File | TypeInfos)
File	     : ソースプログラムのファイルを表す．File にはプログラミン
 	       グ言語によって規定されている文法に即して記述されたソー
	       スプログラムが収められている．型情報を付加しない場合，
	       この要素は CX-model XML文書のルートノードとなる．
	       Child nodes:
	       (Define | Include | Function | Global | Typedecl |
	        Prototype | Tag | Label | comment | op | pp |
	        no_expand | sp | nl | T)
	       Attributes: @id
Define	     : マクロ定義を表す．``#define'' から改行まで．
	       Child nodes:
	       ((kw | sp | comment | macroPattern | macroBody)
Include	     : インクルード文を表す．``#include'' から ``"'' or ``>''
	       まで．
	       Child nodes:
	       (kw | sp | comment | nl | hfile)
Function     : 関数定義を表す．
	       Child nodes:
	       (Define | Type | Tag | Param | Argument | Local | Stmt | flow | Prototype
	        | macroCall | Label | ident | comment
	        | literal | pp | no_expand | kw | sp | op | nl)
	       Attributes: @id
Global	     : 大域変数宣言を表す．
	       Child nodes:
	       (Type | ident | Member | Stmt | flow | literal
	        | macroCall | kw | sp | op | nl | comment)
	       Attributes: @id, @defid
Local	     : 局所変数宣言を表す．
	       Child nodes:
	       (Type | Stmt | flow | ident | literal | macroCall | kw | sp | 
	        op | nl | comment)
	       Attributes: @id, @defid
Argument     : 仮引数宣言を表す．
	       Child nodes:
	       (macroCall | Type | ident | kw | sp | op | nl |
	        comment)
	       Attributes: @id
Typedecl     : typedef 宣言を表す．
	       Child nodes:
	       (Typedecl | Member | Enum | Type | ident |
	        literal |  kw | sp | op | nl | comment)
	       Attributes: @id
Prototype    : プロトタイプ宣言を表す．
	       Child nodes:
	       (Type | Param | Argument | ident | macroCall
	        | comment | pp | no_expand | kw | sp | op | nl)
	       Attributes: @defid
Param	     : 関数定義の括弧内のカンマ (`,') で区切られた 1 つ 1 つを
	       表す．
	       Child nodes:
	       (Type | ident | kw | sp | op | nl | comment)
	       Attributes: @id
Type	     : 型を表す．
	       Child nodes:
	       (ident | kw | op | nl | comment)
Tag	     : タグを表す．(struct から `}' まで)
	       Child nodes:
	       (ident | Enum | Member | pp | no_expand | kw | sp | op 
	        | nl | comment)
	       Attributes: @id
Member	     : メンバ変数を表す
	       Child nodes:
	       (Tag | Type | Member | MacroCall | ident | Expr | liter
	        al | kw | sp | op | nl | comment)
	       Attributes: @id
Enum	     : 列挙子を表す
	       Child nodes:
	       (Type | ident | Expr | kw | sp | op | nl | comment)
	       Attributes: @id
Stmt	     : 文を表す．`{', `}' で囲まれたブロック，if, else, while,
	       for, switch do-while ブロック，`;' までの式
	       Child nodes:
	       (Stmt | flow | Expr | Local | macroCall | literal | Label | pp
	       | no_expand | kw | sp | op | nl | comment)
	       Attributes: @sort
Expr	     : 式を表す．
	       Child nodes:
	       (Expr | Type | Label | macroCall | literal |
	        ident | kw | sp | op | nl | comment | pp | no_expand)
	       Attributes: @type_id
Label	     : ラベルを表す.
	       Child nodes:
	       (kw | sp | literal | ident | Stmt | flow | macroCall)
TypeInfos    : 型情報をまとめる要素．型情報を付加しない場合，この要素は
	       出力されない．
	       Child nodes:
	       (TypeInfo)
TypeInfo     : 1つの型を表す要素．sort属性はこの型が構造体，共用体，列
	       挙体，typedef型，基本型，ポインタ型，配列型，関数型，省
	       略可能引数のどれであるかを表す．ref属性は，この型がtype
	       def型である場合には本来の型，この型がポインタ型である場
	       合にはポイントする型，この型が配列型である場合には格納す
	       る型，この型が関数型である場合には戻り値の型のIDを表す．
	       この型が構造体，共用体，列挙体である場合はこの型のメンバ
	       ，この型が関数型である場合にはこの型の引数を，TypeRef要
	       素を子に持つことで表す．
	       Child nodes:
	       (TypeRef)
	       Attributes: @id, @sort, @const, @volatile, @name,
	       @type, @sign, @size, @ref, @text
TypeRef	     : 型への参照を表す要素．sort属性はこの参照がメンバ、引数の
	       どちらであるかを表す．ref属性はこの参照が参照する型のID
	       を表す．
	       Attributes: @sort, @ref
flow	     : コントロールフローとデータフローを表す．詳細は 3.3で後述
               する．
	       Attributes: @id, @stmt_id, @next, @sort, @expr_id,
	       @var_id
hfile	     : ヘッダファイルを表す．
	       Attributes: @id, @ref
macroPattern : マクロ名を表す．
	       Attributes: @id
macroBody    : マクロ本体を表す．
macroCall    : マクロ呼び出しを表す．
	       Attributes: @defid
ident	     : 識別子を表す．
	       Attributes: @defid, @sort, @type_id
literal	     : リテラルを表す．
	       Attributes: @defid
comment	     : コメントを表す．
op	     : 演算子を表す．
pp	     : プリプロセッサで展開される部分を表す．
no_expand    : プリプロセッサで展開されない部分を表す．
sp	     : 空白文字を表す．
	       Attributes: @sort, @length
nl	     : 改行文字を表す．
	       Attributes: @line, @offset
kw	     : キーワードを表す．
	       Attributes: @sort
T	     : offsetのずれによりできてしまうテキストを暫定的に表す．

3.2 属性一覧

id	     : 識別番号
defid	     : 定義の識別番号
line	     : 行番号
offset       : オフセット
type_id      : この識別子または式の型の識別番号
text	     : この型の，人間向けの文字列表現
const	     : この型が型修飾子constによって修飾されているかどうか
volatile     : この型が型修飾子volatileによって修飾されているかどうか
name	     : この型の名前
type	     : この基本型の種類
sign	     : この基本型の符号の有無
size	     : この基本型の長さ
sort	     : 要素の種類
ref	     : この型，または型への参照が参照する型の識別番号
stmt_id	     : フローの発端となるステートメントの識別番号
next	     : フローの依存先の Stmt 要素の識別番号
expr_id	     : 変数の依存先の Expr の識別番号
dep_id	     : 変数の識別番号

3.3 flow 要素

以下に，flow 要素の説明を示す．また， Attributes には，ノードの属性を@
で列挙している．

flow 要素はコントロールフローとデータフローを表す．弟には flow 要素か
Stmt 要素が必ずくる．弟の中における最初の Stmt 要素のフロー情報を表す．
@id は，flow 要素の識別子．@stmt_id はフローの発端となるステートメント
の識別番号，つまり弟の中における最初の Stmt 要素の識別番号のこと．
@next はフローの依存先の Stmt 要素の識別番号．@sort はそのフローの種類
を表す．詳しくは後述．ここで，属性 sort が data_dependence であるときの
み属性expr_id と属性 dep_id は存在し，それぞれ 変数の依存先の Expr の識
別番号と変数の識別番号を示す．

Attributes : @id @stmt_id @next @sort @expr_id @dep_id


[各 sort 属性の値について例を挙げて説明する]

(1) control_normal : 下記以外の制御フローを表す一般的な制御フロー．

((1-例 source code))

  res = x + 1;  // statement id = "s58720260"
  res = res * 10;  // statement id = "s58720265"

((1-例 XML))
<flow id="f005" stmt_id="s58720260" next="s58720265" sort="control_normal" />
<Stmt id="s58720260">...</Stmt>
<op>;</op>
<nl line="5" offset="47"></nl>
<sp></sp>
<flow id="f004" stmt_id="s58720265" next="s58720267" sort="control_normal" />
<Stmt id="s58720265">...</Stmt>
<op>;</op>


(2) branch_true : for, while, do-while, if の条件が真の場合のフロー．例
    として if 文を挙げる．

(3) branch_false : for, while, do-while, if の条件が偽の場合のフロー．
    例として if 文を挙げる．


    ((2,3-例 soure code))

      if (x>0)  // statement id = "s50331707"
      {  // statement id = "s50331704"
        y = x;  // statement id = "s58720465"
      } else
      {  // statement id = "s50331706"
        y = x;  // statement id = "s58720468"
      }
      z = y;  // statement id = "s58720471"

    ((2,3-例 XML))
    <flow id="f139" stmt_id="s50331707" next="s50331704" sort="branch_true" />
    <flow id="f138" stmt_id="s50331707" next="s50331706" sort="branch_false" />
    <Stmt sort="If" id="s50331707">
      <kw sort="Stmt">if</kw>
      ...
      <flow id="f145" stmt_id="s50331704" next="s58720465" sort="control_normal" />
      <Stmt sort="block" id="s50331704">
        <op>{</op>
        ...
        <flow id="f144" stmt_id="s58720465" next="s58720471" sort="control_normal" />
        <Stmt id="s58720465">...</Stmt>
        <op>;</op>
        ...
        <op>}</op>
      </Stmt>
      <sp></sp>
      <kw>else</kw>
      <sp></sp>
      <flow id="f142" stmt_id="s50331706" next="s58720468" sort="control_normal" />
      <Stmt sort="block" id="s50331706">
        <op>{</op>
        ...
        <flow id="f141" stmt_id="s58720468" next="s58720471" sort="control_normal" />
        <Stmt id="s58720468">...</Stmt>
        <op>;</op>
        ...
        <op>}</op>
      </Stmt>
    </Stmt>
    ...
    <flow id="f136" stmt_id="s58720471" next="s58720473" sort="control_normal" />
    <Stmt id="s58720471">...</Stmt>
    <op>;</op>

(4) loopback : for, while, do-while の最後の文から繰り返しの最初の文へ
    のフロー．例として while 文を挙げる．

    ((4-例 soure code))

      while (x<10)  // statement id = "s50331732"
      {  // statement id = "s50331731"
        x = x + 1;  // statement id = "s58720543"
      }

    ((4-例 XML))
    <flow id="f195" stmt_id="s50331732" next="s50331731" sort="branch_true" />
    <flow id="f194" stmt_id="s50331732" next="s58720546" sort="branch_false" />
    <Stmt sort="While" id="s50331732">
      <kw sort="Stmt">while</kw>
      <sp></sp>
      <op>(</op>
      <Expr id="e58720538">...</Expr>
      <op>)</op>
      <sp></sp>
      <flow id="f198" stmt_id="s50331731" next="s58720543" sort="control_normal" />
      <Stmt sort="block" id="s50331731">
        <op>{</op>
        ...
        <flow id="f197" stmt_id="s58720543" next="s50331732" sort="loopback" />
        <Stmt id="s58720543">...</Stmt>
        <op>;</op>
        <nl line="6" offset="68"></nl>
        <sp></sp>
        <op>}</op>
      </Stmt>
    </Stmt>


(5) switch_case : CASE ラベルの始めの実行文へのフロー．例を挙げる．例の
    ように実行文が一つもない case も存在するため注意が必要．

(6) switch_default : default ラベルの始めの実行文へのフロー．例を挙げる．

    ((5,6-例 soure code))

      switch (i)  // statement id = "s50331726"
      {
        case 0:
          x = i + 1;  // statement id = "s58720514"
          break;  // statement id = "s58720515"
        case 1: 
        case 2:
          i = 10;  // statement id = "s58720520"
          break;  // statement id = "s58720521"
      default:
          x = i + 100;  // statement id = "s58720526"
          break;  // statement id = "s58720527"
      }

    ((5,6-例 XML))
    <flow id="f176" stmt_id="s50331726" next="s58720526" sort="switch_default" />
    <flow id="f175" stmt_id="s50331726" next="s58720514" sort="switch_case" />
    <flow id="f174" stmt_id="s50331726" next="s58720520" sort="switch_case" />
    <Stmt sort="Switch" id="s50331726">
      <kw sort="Stmt">switch</kw>
      ...
        <ident defid="s33554486">i</ident>
      ...
      <Stmt sort="block" id="s50331725">
        <op>{</op>
        ...
        <Label>
          <kw sort="label">case</kw>
          <sp></sp>
          <literal defid="s75497515">0</literal>
        </Label>
        <op>:</op>
        ...
        <flow id="f186" stmt_id="s58720514" next="s58720515" sort="control_normal" />
        <Stmt id="s58720514">...</Stmt>
        <op>;</op>
        ...
        <flow id="f185" stmt_id="s58720515" next="s58720530" sort="control_normal" />
        <Stmt id="s58720515">...</Stmt>
        <op>;</op>
        ...
        <Label>
          <kw sort="label">case</kw>
          <sp></sp>
          <literal defid="s75497514">1</literal>
        </Label>
        <op>:</op>
        ...
        <Label>
          <kw sort="label">case</kw>
          <sp></sp>
          <literal defid="s75497518">2</literal>
        </Label>
        <op>:</op>
        ...
        <flow id="f184" stmt_id="s58720520" next="s58720521" sort="control_normal" />
        <Stmt id="s58720520">...</Stmt>
        <op>;</op>
        ...
        <flow id="f183" stmt_id="s58720521" next="s58720530" sort="control_normal" />
        <Stmt id="s58720521">...</Stmt>
        <op>;</op>
        ...
        <Label>
          <kw sort="label">default</kw>
        </Label>
        <op>:</op>
        ...
        <flow id="f181" stmt_id="s58720526" next="s58720527" sort="control_normal" />
        <Stmt id="s58720526">...</Stmt>
        <op>;</op>
        ...
        <flow id="f180" stmt_id="s58720527" next="s58720530" sort="control_normal" />
        <Stmt id="s58720527">...</Stmt>
        <op>;</op>
        ...
        <op>}</op>
        </Stmt>
    </Stmt>


(7) data_dependence : データフローを表す．属性 sort が data_dependence
    であるときのみ属性 expr_id と属性 dep_id は存在し，それぞれ 変数の依存
    先の Expr の識別子と変数の識別子を示す．例を挙げる．

    ((7-例 soure code))

      x = x + 1;  // statement id = "s58720272"
      res = x * 10;  // statement id = "s58720281"

    ((7-例 XML))
    <flow id="f007" stmt_id="s58720272" next="s58720281" sort="data_dependence" expr_id="e58720274" dep_id="s33554435" />
    <Stmt id="s58720272">...</Stmt>
    <op>;</op>
    ...
    <flow id="f014" stmt_id="s58720281" next="s58720288" sort="data_dependence" expr_id="e58720285" dep_id="s33554435" />
    <Stmt id="s58720281">
      <Expr id="e58720281">
        <Expr id="e58720273">
          <ident defid="s33554437">res</ident>
        </Expr>
        <sp></sp>
        <op>=</op>
        <sp></sp>
        <Expr id="e58720276">
          <Expr id="e58720274">
            <ident defid="s33554435">x</ident>
          </Expr>
          <sp></sp>
          <op>*</op>
          <sp></sp>
          <literal defid="s75497475">10</literal>
        </Expr>
      </Expr>
    </Stmt>

------------------------------

4 問題

(1) 一部のモデル要素に対してoffsetがずれる．

(2) offsetのずれによりできてしまうテキストを暫定的にタグTにより表している．
