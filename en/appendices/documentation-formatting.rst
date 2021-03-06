Documentation formatting guide
##############################

The new CakePHP documentation is written with ReST formatted text.  ReST 
(Re Structured Text) is a plain text markup syntax similar to markdown, or textile.
To maintain consistency it is recommended that when adding to the CakePHP documentation
you follow the guidelines here on how to format and structure your text.

Headings and Sections
=====================

Section headers are created by underlining the title with punctuation characters at 
least the length of the text.

- ``#`` Is used to denote page titles.
- ``=`` Is used for sections in a page.
- ``-`` Is used for subsections.
- ``~`` Is used for sub-subsections
- ``^`` Is used for sub-sub-sections.

Headings should not be nested more than 5 levels deep. Headings should be preceded and followed
by a blank line.

Paragraphs
==========

Paragraphs are simply blocks of text, with all the lines at the same level of indentation.
Paragraphs should be separated by more than one empty line.

Inline markup
=============

* one asterisk: *text* for emphasis (italics),
* two asterisks: **text** for strong emphasis (boldface), and
* backquotes: ``text`` for code samples.

If asterisks or backquotes appear in running text and could be confused with inline markup 
delimiters, they have to be escaped with a backslash.

Inline markup has a few restrictions:

* It **may not** be nested.
* Content may not start or end with whitespace: ``* text*`` is wrong.
* Content must be separated from surrounding text by non-word characters. Use a backslash escaped space to work around that: ``onelong\ *bolded*\ word``.

Lists
=====

List markup is very similar to markdown.  Unordered lists are indicated by starting a line with a single asterisk and a space.  Numbered lists can be created with either numerals, or ``#`` for auto numbering::

    * This is a bullet
    * So is this.  But this line
      has two lines.
      
    1. First line
    2. Second line
    
    #. Automatic numbering
    #. Will save you some time.

Indented lists can also be created, by indenting sections and separating them with an empty line::

    * First line
    * Second line
    
        * Going deeper
        * Whoah
    
    * Back to the first level.

Definition lists can be created by doing the following::

    term
        definition
    CakePHP
        An MVC framework for PHP

Terms cannot be more than one line, but definitions can be multi-line and all lines should be indented consistently.

Links
=====

There are several kinds of links, each with their own uses.

External links
--------------

Links to external documents can be with the following::

    `External Link <http://example.com>`_

The above would generate a link pointing to http://example.com

Links to other pages
--------------------

.. rst:role:: doc

    Other pages in the documentation can be linked to using the ``:doc:`` role. 
    You can link to the specified document using either an absolute or relative path reference.  
    You should omit the ``.rst`` extension.  For example, if the reference ``:doc:`form``` appears in 
    the document ``core-helpers/html``, then the link references ``core-helpers/form``.  
    If the reference was ``:doc:`/core-helpers```, it would always reference ``/core-helpers`` regardless
    of where it was used.

Cross referencing links
-----------------------

.. rst:role:: ref

    You can cross reference any arbitrary title in any document using the ``:ref:`` role.  Link label targets
    must be unique across the entire documentation.  When creating labels for class methods, its best to use 
    ``class-method`` as the format for your link label.
    
    The most common use of labels is above a title.  Example::
    
        .. _label-name:
        
        Section heading
        ---------------
        
        More content here.
    
    Elsewhere you could reference the above section using ``:ref:`label-name```.  The link's text would be the
    title that the link preceded.  You can also provide custom link text using ``:ref:`Link text <label-name>```.

Describing classes and their contents
=====================================

The CakePHP documentation, uses the `phpdomain <http://pypi.python.org/pypi/sphinxcontrib-phpdomain>` 
to provide custom directives for describing PHP objects and constructs.  Using these directives
and roles is required to give proper indexing and cross referencing features.

Describing classes and constructs
---------------------------------

Each directive populates the index, and or the namespace index.

.. rst:directive:: .. php:global:: name

   This directive declares a new PHP global variable.

.. rst:directive:: .. php:function:: name(signature)

   Defines a new global function outside of a class.

.. rst:directive:: .. php:const:: name

   This directive declares a new PHP constant, you can also used it nested 
   inside a class directive to create class constants.
   
.. rst:directive:: .. php:exception:: name

   This directive declares a new Exception in the current namespace. The 
   signature can include constructor arguments.

.. rst:directive:: .. php:class:: name

   Describes a class.  Methods, attributes, and constants belonging to the class
   should be inside this directive's body::

        .. php:class:: MyClass
        
            Class description
        
           .. php:method:: method($argument)
        
           Method description


   Attributes, methods and constants don't need to be nested.  They can also just 
   follow the class declaration::

        .. php:class:: MyClass
        
            Text about the class
        
        .. php:method:: methodName()
        
            Text about the method
        

   .. seealso:: .. php:method:: name
                .. php:attr:: name
                .. php:const:: name

.. rst:directive:: .. php:method:: name(signature)

   Describe a class method, its arguments, return value, and exceptions::
   
        .. php:method:: instanceMethod($one, $two)
        
            :param string $one: The first parameter.
            :param string $two: The second parameter.
            :returns: An array of stuff.
            :throws: InvalidArgumentException
        
           This is an instance method.

.. rst:directive:: .. php:staticmethod:: ClassName::methodName(signature)

    Describe a static method, its arguments, return value and exceptions,
    see :rst:dir:`php:method` for options.

.. rst:directive:: .. php:attr:: name

   Describe an property/attribute on a class.

Cross Referencing
-----------------

The following roles refer to php objects and are links are generated if a 
matching directive is found:

.. rst:role:: php:func

   Reference a PHP function.

.. rst:role:: php:global

   Reference a global variable whose name has ``$`` prefix.
   
.. rst:role:: php:const

   Reference either a global constant, or a class constant.  Class constants should
   be preceded by the owning class::
   
        DateTime has an :php:const:`DateTime::ATOM` constant.

.. rst:role:: php:class

   Reference a class by name::
   
     :php:class:`ClassName`

.. rst:role:: php:meth

   Reference a method of a class. This role supports both kinds of methods::
   
     :php:meth:`DateTime::setDate`
     :php:meth:`Classname::staticMethod`

.. rst:role:: php:attr

   Reference a property on an object::
   
      :php:attr:`ClassName::$propertyName`

.. rst:role:: php:exc

   Reference an exception.


Source code
===========

Literal code blocks are created by ending a paragraph with ``::``. The literal block must be indented, and like
all paragraphs be separated by single lines::

    This is a paragraph
        
        while ($i--) {
            doStuff()
        }
    
    This is regular text again.

Literal text is not modified or formatted, save that one level of indentation is removed.


Notes and warnings
==================

There are often times when you want to inform the reader of an important tip, special note or a potential hazard. Admonitions in sphinx are used for just that.  There are three kinds of admonitions. 

* ``.. tip::`` Tips are used to document or re-iterate interesting or important information. 
  The content of the directive should be written in complete sentences and include all appropriate punctuation.
* ``.. note::`` Notes are used to document an especially important piece of information. 
  The content of the directive should be written in complete sentences and include all appropriate punctuation.
* ``.. warning::`` Warnings are used to document potential stumbling blocks, or information pertaining to security.
  The content of the directive should be written in complete sentences and include all appropriate punctuation.
  
All admonitions are made the same::

    .. note::
    
        Indented and preceeded and followed by a blank line. Just like a paragraph.
    
    This text is not part of the note.

Samples
-------

.. tip::

    This is a helpful tid-bit you probably forgot.

.. note::

    You should pay attention here.

.. warning::

    It could be dangerous.
