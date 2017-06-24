# JohnLBevan.github.io
## Project Ideas
### Create XSLT2.0 Monkey Patch stylesheet.

Currently MS XslCompiledTransform only supports XSLT 1.0.
To get XSLT 2.0 support you need to change engine to something like Saxon 9 (http://saxon.sourceforge.net/).

The idea of this project is to avoid the need to swtich engines; rather have an XSLT file with a `msxsl:script language="C#"` block defining these XSLT 2.0 functions.
We could then add the line `<"xsl:include" href="Xslt20MonkeyPatch.xsl" />` to pull in these definitions and thus duck punch our XSL into the 21st centuary.

Example:

```xsl
<!-- Script to check for URLs in values -->
<msxsl:script language="C#" implements-prefix="xslt2ish">
    <![CDATA[
      public string format-date(DateTime date, string format)
      {
          return string.Format(date, format); //we'd actually write code here to work per XSLT 2.0 definitions; i.e. http://www.sixtree.com.au/articles/2013/formatting-dates-and-times-using-xslt-2.0-and-xpath/
      }
	  public object max (params object[] args) 
	  {
		return args.Max();
	  }
    ]]>
</msxsl:script>
```
