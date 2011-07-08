# Inline Erlsom

This is a parse-transform extension for the 
[inline_xml](https://github.com/hyperthunk/inline_xml) utility, adding explicit 
support for the erlsom XML parser and its various features.

## Usage

Use of XML schemas (for use in erlsom's data binding mode) is supported. You can
enable this support by including the requisite header file and declaring your XSD
files in the following manner.

```erlang
-module(custom).
-import_xsd(["priv/xsd/models.xsd"]).
-include_lib("inline_xml/include/inline_erlsom.hrl").
```

When you import an XSD, the file is processed (at build time) and an Erlang header
file with record definitions (for data binding) produced by erlsom. The header(s)
will then be imported into your module automatically. Your code, after being 
transformed, will look something like:

```erlang
-module(custom).
-include("models.hrl").
-include_lib("inline_xml/include/inline_erlsom.hrl").
%% etc ....
```


Any XML that is being inlined (i.e., XML being processed by the parse transform in
[inline_xml](https://github.com/hyperthunk/inline_xml)) will be processed using 
the erlsom functions that work with these data bindings. Again, this takes place 
at compile time, so your literal XML will be validated against the given schema
before your code can be built.
