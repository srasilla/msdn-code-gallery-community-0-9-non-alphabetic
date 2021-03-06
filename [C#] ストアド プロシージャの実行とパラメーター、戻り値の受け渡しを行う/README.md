# [C#] ストアド プロシージャの実行とパラメーター、戻り値の受け渡しを行う
## License
- Apache License, Version 2.0
## Technologies
- Visual Studio 2008
- Visual Studio 2010
- Visual Studio 2005
- .NET Framework 4
- .NET Framework 2.0
- .NET Framework 3.0
- .NET Framework 3.5
## Topics
- データ アクセス開発
- 逆引きサンプル コード
## Updated
- 02/22/2011
## Description

<p>執筆者: <a href="http://msdn.microsoft.com/ja-jp/gg585574#kodaka" target="_blank">
インフォシェア株式会社 小高 太郎</a></p>
<p>動作確認環境:&nbsp;.NET Framework2.0 以上、Visual Studio 2005 以上</p>
<hr style="clear:both; margin-bottom:8px; margin-top:20px">
<p>ADO.NET でストアド プロシージャを呼び出すには Command オブジェクトを用います。このときパラメーターや戻り値の受け渡しには、その種類によっていくつかの手法が存在します。ここでは代表的な手法についてご紹介します。</p>
<p class="1">あらかじめ、SQL Server のサンプル データベース Northwind に、以下のストアド プロシージャを作成しておきます。</p>
<div style="margin:20px 0px; padding:10px; background-color:#cccccc">CREATE PROCEDURE [dbo].[Most Expensive Products]<br>
@COUNT INT,<br>
@SUM INT OUTPUT<br>
AS<br>
SET ROWCOUNT @COUNT<br>
&nbsp;<br>
SELECT @SUM = SUM(Products.UnitPrice)FROM Products<br>
SELECT Products.ProductName, Products.UnitPrice FROM Products<br>
RETURN 0</div>
<p>このストアド プロシージャは、インプット引数、アウトプット引数、結果セット、戻り値と 4 種類の情報を受け渡しするようになっています。</p>
<p>上記のストアド プロシージャを呼び出すコードは以下のようになります。</p>
<div>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginEditHolderLink">スクリプトの編集</div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/ja-JP/library/System.Data.SqlClient.aspx" target="_blank" title="Auto generated link to System.Data.SqlClient">System.Data.SqlClient</a>;&nbsp;
<span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/ja-JP/library/System.Data.aspx" target="_blank" title="Auto generated link to System.Data">System.Data</a>;&nbsp;
&nbsp;
<span class="cs__keyword">static</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Main(<span class="cs__keyword">string</span>[]&nbsp;args)&nbsp;
{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">using</span>&nbsp;(SqlConnection&nbsp;cn&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;SqlConnection())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cn.ConnectionString&nbsp;=&nbsp;@<span class="cs__string">&quot;Data&nbsp;Source=.;Initial&nbsp;Catalog=Northwind;Integrated&nbsp;Security=True&quot;</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cn.Open();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SqlCommand&nbsp;cmd&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;SqlCommand(<span class="cs__string">&quot;Most&nbsp;Expensive&nbsp;Products&quot;</span>,&nbsp;cn);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.CommandType&nbsp;=&nbsp;CommandType.StoredProcedure;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters.Add(<span class="cs__keyword">new</span>&nbsp;SqlParameter(<span class="cs__string">&quot;COUNT&quot;</span>,&nbsp;SqlDbType.Int));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters[<span class="cs__string">&quot;COUNT&quot;</span>].Direction&nbsp;=&nbsp;ParameterDirection.Input;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters[<span class="cs__string">&quot;COUNT&quot;</span>].Value&nbsp;=&nbsp;<span class="cs__number">10</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters.Add(<span class="cs__keyword">new</span>&nbsp;SqlParameter(<span class="cs__string">&quot;SUM&quot;</span>,&nbsp;SqlDbType.Int));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters[<span class="cs__string">&quot;SUM&quot;</span>].Direction&nbsp;=&nbsp;ParameterDirection.Output;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters.Add(<span class="cs__keyword">new</span>&nbsp;SqlParameter(<span class="cs__string">&quot;ReturnValue&quot;</span>,&nbsp;SqlDbType.Int));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cmd.Parameters[<span class="cs__string">&quot;ReturnValue&quot;</span>].Direction&nbsp;=&nbsp;ParameterDirection.ReturnValue;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SqlDataReader&nbsp;dr&nbsp;=&nbsp;cmd.ExecuteReader();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">while</span>&nbsp;(dr.Read())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(<span class="cs__string">&quot;結果セット:&quot;</span>&nbsp;&#43;&nbsp;dr[<span class="cs__number">0</span>]);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dr.Close();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;returnValue&nbsp;=&nbsp;((<span class="cs__keyword">int</span>)cmd.Parameters[<span class="cs__string">&quot;ReturnValue&quot;</span>].Value);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(<span class="cs__string">&quot;戻り値:&quot;</span>&nbsp;&#43;&nbsp;returnValue.ToString());&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;sum&nbsp;=&nbsp;((<span class="cs__keyword">int</span>)cmd.Parameters[<span class="cs__string">&quot;SUM&quot;</span>].Value);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(<span class="cs__string">&quot;アウトプット引数:&quot;</span>&nbsp;&#43;&nbsp;sum.ToString());&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
}&nbsp;
&nbsp;
</pre>
</div>
</div>
</div>
</div>
<p>このコードでは、結果セットを取得するために ExecuteReader メソッドでストアド プロシージャを実行し、その戻り値を DataReader として受けます。戻り値やアウトプット引数を取得する前に、DataReader を Close する必要があります。</p>
<p>今回は、複数行、複数列が存在する結果セットでしたが、結果セットが 1 行 1 列の場合、ExecuteScalar で実行する事も可能です。また、結果セットが必要ないのであれば、ExecuteNonQuery での実行も可能です。(結果セットが存在しても ExecuteScalar や ExecuteNonQuery でのストアド プロシージャ実行は可能ですが、その場合、返される行は破棄されます。)</p>
<p>更に非接続型の DataSet(DataTable) で結果セットを受け取る事も可能です。上記の&nbsp;SqlDataReader dr = cmd.ExecuteReader(); から、dr.Close(); までを以下にように変更します。</p>
<div>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginEditHolderLink">スクリプトの編集</div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">SqlDataAdapter&nbsp;da&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;SqlDataAdapter&nbsp;(cmd);&nbsp;
DataSet&nbsp;ds&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;DataSet&nbsp;();&nbsp;
da.Fill(ds);&nbsp;
<span class="cs__keyword">foreach</span>&nbsp;(DataRow&nbsp;rw&nbsp;<span class="cs__keyword">in</span>&nbsp;ds.Tables[<span class="cs__number">0</span>].Rows)&nbsp;
{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(<span class="cs__string">&quot;結果セット:&quot;</span>&nbsp;&#43;&nbsp;rw[<span class="cs__number">0</span>].ToString());&nbsp;
}&nbsp;
&nbsp;
</pre>
</div>
</div>
</div>
</div>
<p>上記の実行結果は以下になります。</p>
<p><img src="18599-image001.gif" alt="図 1" width="368" height="230"></p>
<h2 style="margin-top:30px">参考リンク</h2>
<ul>
<li><a href="http://msdn.microsoft.com/ja-jp/library/tyy0sz6b.aspx" target="_blank">コマンドの実行 (ADO.NET)</a>
</li><li><a href="http://msdn.microsoft.com/ja-jp/library/yy6y35y8%28v=vs.80%29.aspx" target="_blank">コマンドによるストアド プロシージャの使用</a>
</li><li><a href="http://msdn.microsoft.com/ja-jp/library/yy6y35y8.aspx" target="_blank">パラメーターおよびパラメーターのデータ型の構成 (ADO.NET)</a>
</li></ul>
<hr style="clear:both; margin-bottom:8px; margin-top:20px">
<table>
<tbody>
<tr>
<td><a href="http://msdn.microsoft.com/ja-jp/samplecode.recipe"><img src="http://i.msdn.microsoft.com/ff950935.coderecipe_180x70%28ja-jp,MSDN.10%29.jpg" border="0" alt="Code Recipe" width="180" height="70" style="margin-top:3px"></a></td>
<td>
<ul>
<li>もっと他のコンテンツを見る &gt;&gt; <a href="http://msdn.microsoft.com/ja-jp/ff363212" target="_blank">
逆引きサンプル コード一覧へ</a> </li><li>もっと他のレシピを見る &gt;&gt; <a href="http://msdn.microsoft.com/ja-jp/samplecode.recipe">
Code Recipe へ</a> </li></ul>
</td>
</tr>
</tbody>
</table>
<p style="margin-top:20px"><a href="#top"><img src="http://www.microsoft.com/japan/msdn/nodehomes/graphics/top.gif" border="0" alt="">ページのトップへ</a></p>
