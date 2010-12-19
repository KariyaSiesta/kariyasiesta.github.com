チュートリアル
=======================

SDB の作成
-----------------------
SDB はソフトウェアデータベースの略で、C言語ソースコードの解析結果を保存しています。
KariyaSiesta はソースコードのチェックに SDB を利用しているため、
チェックの前に SDB を構築する必要があります。

**Project Explorer** からチェックしたいプロジェクトの Makefile を右クリックし、
**KariyaSiesta** -> **Create SDB** をクリックします。

.. image:: _static/tutorial_sdb1.png
.. image:: _static/tutorial_sdb2.png

これで SDB の構築は終了です。
ソースコードを変更するたびに、SDB 構築が必要です。

XPathViwer の使い方
-----------------------

**Window** -> **Show View** -> **Other...** をクリックし、
**KariyaSiesta** 内の **XPath Viewer** をクリックします。 **OK** をクリッ
クします。

.. image:: _static/tutorial01.png

表示された XPathViwer 内のテキストエリアにチェックしたいルールを表す
XPath 式を入力して TAB キーを押すと、ソースコードの該当部分にマーカが表示されます。

.. image:: _static/tutorial02.png

XPathViwer 内のボタンの機能は以下の通りです。

**Clear:**
  テキストエリアに入力した XPath 式が削除されます。
**Get:**
  エディタでソースコードの一部を選択し Get ボタンを押すと、
  その部分の XPath 式がテキストエリアに出力されます。
**Copy:**
  入力した XPath 式に対応するルール設定ファイルがクリップボードにコピーされます。


XPath によるルールの作成方法
-----------------------------
KariyaSiesta では、ソースコードに対するルールを CX-Model 形式の
XML の構造に対するルールで表現します。
CX-Model については `ドキュメント <_static/README-CX-model.ja.txt>`_ を参照してください。

例えば、while ブロック内部で break を使ってはいけないというルールは
以下のように書くことができます。 ::
  //Stmt[@sort="While" and .//keyword[text()="break"]]



ルールの設定方法
-----------------------
複数のルールをチェックしたい場合は、ルール設定ファイルを作成します。
上記のルールのルール設定ファイルの内容は、例えば以下のようになります。 ::

  <?xml version="1.0" encoding="UTF-8"?>
  <rules>
    <oneRule>
      <level>3</level>
      <content>while ブロック内部で break を使ってはいけない</content>
      <xpath>//Stmt[@sort="While" and .//kw[text()="break"]]</xpath>
      <condition>require</condition>
    </oneRule>
  </rules>

タグの意味は以下の通りです。

**level**
  ルールの重要度を表します。ただし現在は重要度を扱うことができないため
  空でない任意の値を設定してください。
**content**
  ルールの名前です。
**xpath**
  ルールを表現する XPath 式です。
**condition**
  *require* か *prohibit* を指定します。
  *require* を指定した場合は、 XPath 式にマッチする要素がある場合にマーカが表示されます。
  *prohibit* を指定した場合は、 XPath 式にマッチする要素がない場合にマーカが表示されます。

ルール設定ファイルを作成したら、ルール設定ファイルを KariyaSiesta に登録します。
**Project Explorer** からプロジェクトを右クリックし、 **Properties** をクリックします。
**KariyaSiesta** をクリックします。

.. image:: _static/tutorial_property.png

**XPath Rule XML (WorkSpace)** 内の **New...** をクリックします。
ルール設定ファイルを置いたディレクトリを選択し、 ***OK*** をクリックします。


チェック方法
-----------------------
**Project Explorer** からチェックしたいプロジェクトを右クリックし、
**Check All Files in the Project** をクリックします。

.. image:: _static/tutorial_check.png

プロジェクト内のすべてのファイルに対して、ルール設定ファイルで設定したルールがチェックされます。
