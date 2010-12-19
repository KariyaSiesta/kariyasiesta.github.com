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

�ܼ�:

	1 �Ϥ����
	2 ������ˡ
	3 CX-model
	3.1 CX-model������
	3.2 °������
	3.3 flow ����
	4 ����

==============================

1 �Ϥ����

spdMkCXModel��CX-model�˴�Ť���XML�����Υ�ݥ��ȥ���������륳�ޥ�ɤ�
���롥

���: CX-model�ϳ�ȯ��Ǥ��ꡤ��ǥ����ǡ�°�����ѹ����ɲä�����ǽ����
���롥�ޤ���spdMkCXModel�ϰ����Υ�ǥ����Ǥ��Ф���offset������롥

------------------------------

2 ������ˡ
% spdMkCXModel [options] [target_program]

-d ���ץ�������ꤷ�ʤ���硤SDB�����ۤ���Ƥ���ǥ��쥯�ȥ�Ǽ¹Ԥ�
��ɬ�פ����롥���ϥե�����̾�ϥǥե���ȤǤ� <fileId>.xml �Ǥ��ꡤ-sdbD
���ץ�������ꤷ������ <�������ե�����̾>.xml �Ǥ��롥

���ץ�����ʲ��˼�����
-d directory    : SDB�ǥ��쥯�ȥ�ΰ��֤���ꤹ�롥�ǥե���ȤǤ�"SDB"
�Ǥ��롥
-f              : �ե�������ղä��롥
-h              : �إ�פ�ɽ�����롥
-sdbD directory : XML�ե�����ν��������ꤹ�롥
-t              : ��������ղä��롥
-v              : �ܺ٥�å�������ɽ�����롥
-w              : �ٹ��å�������ɽ�����롥
-D directory    : ���ͥե�����ν��������ꤹ�롥�ǥե���ȤǤ�"SPEC"
�Ǥ��롥
-P              : ��ȥե��������¸���롥
-S directory    : ���󥯥롼�ɥǥ��쥯�ȥ����ꤹ�롥
target_program  : �������åȥץ�������ꤹ�롥�ǥե���ȤǤ�"a.out"
�Ǥ��롥

��������ղä����硤spdMkCXModel�ϥ��֥��ޥ��spdMkCXTypeInfos��¹�
���롥spdMkCXTypeInfos�Ϸ������<�������åȥץ����̾>_typeInfos.xml
�˽��Ϥ����������ַ����Ȥ��ƺ����ɤ߹��ߡ�spdMkCXModel�����Ϥ���CX-
modelʸ����������롥

------------------------------

3 CX-model

3.1 CX-model������

CX	     : ��������ղä������� CX-model XML ʸ��Υ롼�ȥΡ���
	       ��������ղä��ʤ���硤�������ǤϽ��Ϥ���ʤ���
	       Child nodes:
	       (File | TypeInfos)
File	     : �������ץ����Υե������ɽ����File �ˤϥץ���ߥ�
 	       ������ˤ�äƵ��ꤵ��Ƥ���ʸˡ��¨���Ƶ��Ҥ��줿����
	       ���ץ���ब������Ƥ��롥��������ղä��ʤ���硤
	       �������Ǥ� CX-model XMLʸ��Υ롼�ȥΡ��ɤȤʤ롥
	       Child nodes:
	       (Define | Include | Function | Global | Typedecl |
	        Prototype | Tag | Label | comment | op | pp |
	        no_expand | sp | nl | T)
	       Attributes: @id
Define	     : �ޥ��������ɽ����``#define'' ������Ԥޤǡ�
	       Child nodes:
	       ((kw | sp | comment | macroPattern | macroBody)
Include	     : ���󥯥롼��ʸ��ɽ����``#include'' ���� ``"'' or ``>''
	       �ޤǡ�
	       Child nodes:
	       (kw | sp | comment | nl | hfile)
Function     : �ؿ������ɽ����
	       Child nodes:
	       (Define | Type | Tag | Param | Argument | Local | Stmt | flow | Prototype
	        | macroCall | Label | ident | comment
	        | literal | pp | no_expand | kw | sp | op | nl)
	       Attributes: @id
Global	     : ����ѿ������ɽ����
	       Child nodes:
	       (Type | ident | Member | Stmt | flow | literal
	        | macroCall | kw | sp | op | nl | comment)
	       Attributes: @id, @defid
Local	     : �ɽ��ѿ������ɽ����
	       Child nodes:
	       (Type | Stmt | flow | ident | literal | macroCall | kw | sp | 
	        op | nl | comment)
	       Attributes: @id, @defid
Argument     : �����������ɽ����
	       Child nodes:
	       (macroCall | Type | ident | kw | sp | op | nl |
	        comment)
	       Attributes: @id
Typedecl     : typedef �����ɽ����
	       Child nodes:
	       (Typedecl | Member | Enum | Type | ident |
	        literal |  kw | sp | op | nl | comment)
	       Attributes: @id
Prototype    : �ץ�ȥ����������ɽ����
	       Child nodes:
	       (Type | Param | Argument | ident | macroCall
	        | comment | pp | no_expand | kw | sp | op | nl)
	       Attributes: @defid
Param	     : �ؿ�����γ����Υ���� (`,') �Ƕ��ڤ�줿 1 �� 1 �Ĥ�
	       ɽ����
	       Child nodes:
	       (Type | ident | kw | sp | op | nl | comment)
	       Attributes: @id
Type	     : ����ɽ����
	       Child nodes:
	       (ident | kw | op | nl | comment)
Tag	     : ������ɽ����(struct ���� `}' �ޤ�)
	       Child nodes:
	       (ident | Enum | Member | pp | no_expand | kw | sp | op 
	        | nl | comment)
	       Attributes: @id
Member	     : �����ѿ���ɽ��
	       Child nodes:
	       (Tag | Type | Member | MacroCall | ident | Expr | liter
	        al | kw | sp | op | nl | comment)
	       Attributes: @id
Enum	     : ���Ҥ�ɽ��
	       Child nodes:
	       (Type | ident | Expr | kw | sp | op | nl | comment)
	       Attributes: @id
Stmt	     : ʸ��ɽ����`{', `}' �ǰϤޤ줿�֥�å���if, else, while,
	       for, switch do-while �֥�å���`;' �ޤǤμ�
	       Child nodes:
	       (Stmt | flow | Expr | Local | macroCall | literal | Label | pp
	       | no_expand | kw | sp | op | nl | comment)
	       Attributes: @sort
Expr	     : ����ɽ����
	       Child nodes:
	       (Expr | Type | Label | macroCall | literal |
	        ident | kw | sp | op | nl | comment | pp | no_expand)
	       Attributes: @type_id
Label	     : ��٥��ɽ��.
	       Child nodes:
	       (kw | sp | literal | ident | Stmt | flow | macroCall)
TypeInfos    : �������ޤȤ�����ǡ���������ղä��ʤ���硤�������Ǥ�
	       ���Ϥ���ʤ���
	       Child nodes:
	       (TypeInfo)
TypeInfo     : 1�Ĥη���ɽ�����ǡ�sort°���Ϥ��η�����¤�Ρ������Ρ���
	       ���Ρ�typedef�������ܷ����ݥ��󥿷������󷿡��ؿ�������
	       ά��ǽ�����Τɤ�Ǥ��뤫��ɽ����ref°���ϡ����η���type
	       def���Ǥ�����ˤ�����η������η����ݥ��󥿷��Ǥ����
	       ��ˤϥݥ���Ȥ��뷿�����η������󷿤Ǥ�����ˤϳ�Ǽ��
	       �뷿�����η����ؿ����Ǥ�����ˤ�����ͤη���ID��ɽ����
	       ���η�����¤�Ρ������Ρ�����ΤǤ�����Ϥ��η��Υ���
	       �����η����ؿ����Ǥ�����ˤϤ��η��ΰ�����TypeRef��
	       �Ǥ�Ҥ˻��Ĥ��Ȥ�ɽ����
	       Child nodes:
	       (TypeRef)
	       Attributes: @id, @sort, @const, @volatile, @name,
	       @type, @sign, @size, @ref, @text
TypeRef	     : ���ؤλ��Ȥ�ɽ�����ǡ�sort°���Ϥ��λ��Ȥ����С�������
	       �ɤ���Ǥ��뤫��ɽ����ref°���Ϥ��λ��Ȥ����Ȥ��뷿��ID
	       ��ɽ����
	       Attributes: @sort, @ref
flow	     : ����ȥ���ե��ȥǡ����ե���ɽ�����ܺ٤� 3.3�Ǹ��
               ���롥
	       Attributes: @id, @stmt_id, @next, @sort, @expr_id,
	       @var_id
hfile	     : �إå��ե������ɽ����
	       Attributes: @id, @ref
macroPattern : �ޥ���̾��ɽ����
	       Attributes: @id
macroBody    : �ޥ������Τ�ɽ����
macroCall    : �ޥ���ƤӽФ���ɽ����
	       Attributes: @defid
ident	     : ���̻Ҥ�ɽ����
	       Attributes: @defid, @sort, @type_id
literal	     : ��ƥ���ɽ����
	       Attributes: @defid
comment	     : �����Ȥ�ɽ����
op	     : �黻�Ҥ�ɽ����
pp	     : �ץ�ץ��å���Ÿ���������ʬ��ɽ����
no_expand    : �ץ�ץ��å���Ÿ������ʤ���ʬ��ɽ����
sp	     : ����ʸ����ɽ����
	       Attributes: @sort, @length
nl	     : ����ʸ����ɽ����
	       Attributes: @line, @offset
kw	     : ������ɤ�ɽ����
	       Attributes: @sort
T	     : offset�Τ���ˤ��Ǥ��Ƥ��ޤ��ƥ����Ȥ����Ū��ɽ����

3.2 °������

id	     : �����ֹ�
defid	     : ����μ����ֹ�
line	     : ���ֹ�
offset       : ���ե��å�
type_id      : ���μ��̻Ҥޤ��ϼ��η��μ����ֹ�
text	     : ���η��Ρ��ʹָ�����ʸ����ɽ��
const	     : ���η�����������const�ˤ�äƽ�������Ƥ��뤫�ɤ���
volatile     : ���η�����������volatile�ˤ�äƽ�������Ƥ��뤫�ɤ���
name	     : ���η���̾��
type	     : ���δ��ܷ��μ���
sign	     : ���δ��ܷ�������̵ͭ
size	     : ���δ��ܷ���Ĺ��
sort	     : ���Ǥμ���
ref	     : ���η����ޤ��Ϸ��ؤλ��Ȥ����Ȥ��뷿�μ����ֹ�
stmt_id	     : �ե���ȯü�Ȥʤ륹�ơ��ȥ��Ȥμ����ֹ�
next	     : �ե��ΰ�¸��� Stmt ���Ǥμ����ֹ�
expr_id	     : �ѿ��ΰ�¸��� Expr �μ����ֹ�
dep_id	     : �ѿ��μ����ֹ�

3.3 flow ����

�ʲ��ˡ�flow ���Ǥ������򼨤����ޤ��� Attributes �ˤϡ��Ρ��ɤ�°����@
����󤷤Ƥ��롥

flow ���Ǥϥ���ȥ���ե��ȥǡ����ե���ɽ������ˤ� flow ���Ǥ�
Stmt ���Ǥ�ɬ�����롥�����ˤ�����ǽ�� Stmt ���ǤΥե������ɽ����
@id �ϡ�flow ���Ǥμ��̻ҡ�@stmt_id �ϥե���ȯü�Ȥʤ륹�ơ��ȥ���
�μ����ֹ桤�Ĥޤ������ˤ�����ǽ�� Stmt ���Ǥμ����ֹ�Τ��ȡ�
@next �ϥե��ΰ�¸��� Stmt ���Ǥμ����ֹ桥@sort �Ϥ��Υե��μ���
��ɽ�����ܤ����ϸ�ҡ������ǡ�°�� sort �� data_dependence �Ǥ���Ȥ���
��°��expr_id ��°�� dep_id ��¸�ߤ������줾�� �ѿ��ΰ�¸��� Expr �μ�
���ֹ���ѿ��μ����ֹ�򼨤���

Attributes : @id @stmt_id @next @sort @expr_id @dep_id


[�� sort °�����ͤˤĤ������󤲤���������]

(1) control_normal : �����ʳ�������ե���ɽ������Ū������ե���

((1-�� source code))

  res = x + 1;  // statement id = "s58720260"
  res = res * 10;  // statement id = "s58720265"

((1-�� XML))
<flow id="f005" stmt_id="s58720260" next="s58720265" sort="control_normal" />
<Stmt id="s58720260">...</Stmt>
<op>;</op>
<nl line="5" offset="47"></nl>
<sp></sp>
<flow id="f004" stmt_id="s58720265" next="s58720267" sort="control_normal" />
<Stmt id="s58720265">...</Stmt>
<op>;</op>


(2) branch_true : for, while, do-while, if �ξ�郎���ξ��Υե�����
    �Ȥ��� if ʸ��󤲤롥

(3) branch_false : for, while, do-while, if �ξ�郎���ξ��Υե���
    ��Ȥ��� if ʸ��󤲤롥


    ((2,3-�� soure code))

      if (x>0)  // statement id = "s50331707"
      {  // statement id = "s50331704"
        y = x;  // statement id = "s58720465"
      } else
      {  // statement id = "s50331706"
        y = x;  // statement id = "s58720468"
      }
      z = y;  // statement id = "s58720471"

    ((2,3-�� XML))
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

(4) loopback : for, while, do-while �κǸ��ʸ���鷫���֤��κǽ��ʸ��
    �Υե�����Ȥ��� while ʸ��󤲤롥

    ((4-�� soure code))

      while (x<10)  // statement id = "s50331732"
      {  // statement id = "s50331731"
        x = x + 1;  // statement id = "s58720543"
      }

    ((4-�� XML))
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


(5) switch_case : CASE ��٥�λϤ�μ¹�ʸ�ؤΥե������󤲤롥���
    �褦�˼¹�ʸ����Ĥ�ʤ� case ��¸�ߤ��뤿����դ�ɬ�ס�

(6) switch_default : default ��٥�λϤ�μ¹�ʸ�ؤΥե������󤲤롥

    ((5,6-�� soure code))

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

    ((5,6-�� XML))
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


(7) data_dependence : �ǡ����ե���ɽ����°�� sort �� data_dependence
    �Ǥ���Ȥ��Τ�°�� expr_id ��°�� dep_id ��¸�ߤ������줾�� �ѿ��ΰ�¸
    ��� Expr �μ��̻Ҥ��ѿ��μ��̻Ҥ򼨤������󤲤롥

    ((7-�� soure code))

      x = x + 1;  // statement id = "s58720272"
      res = x * 10;  // statement id = "s58720281"

    ((7-�� XML))
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

4 ����

(1) �����Υ�ǥ����Ǥ��Ф���offset������롥

(2) offset�Τ���ˤ��Ǥ��Ƥ��ޤ��ƥ����Ȥ����Ū�˥���T�ˤ��ɽ���Ƥ��롥
