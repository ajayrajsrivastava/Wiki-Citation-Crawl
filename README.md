The user provides the URL of the Wiki article he wants to crawl.
He is provided with two queries :

1-Get Lines which have the given citation.
2-Get Citations of a particular lines.

For query of type '1': All the a-tags which have 'href' attribute of type -> '#cite_note-*\w*-+'+citation+'\$' (Reference Link)
are taken and the text portion of their parent's parent ('sup'->'p'-paragraph) is converted to type 'str' from unicode.The sentence from paragraph('para') is then extracted using another regex pattern.

NOTE:
The extracted text is added to a set (unique elements) and then printed since a paragraph may contain more than one same citation. Also, a defintion setLink() is used in the beginning to add an element '$' in the end of 'href' of all a-tags to denote end of the regex pattern 'refPattern'. Example: #cite_note-Kruger-1 gives #cite_note-Kruger-11,#cite_note-Kruger-12,#cite_note-Kruger-13 etc , therefore,#cite_note-Kruger-1$ is used.

```html
<p> 
    " Paragraph Containing Citation "
    <sup class="reference"> 
        <a href="#cite_note-*\w*-+'+citation+'\$"> </a> 
    </sup> 
</p> 

```
For query of type '2' : Format assumption -> "Lines".[1] or "Lines".[1][2][3]..(Multiple Citations) . Function getCitation(lines) calculates the index of lines in para (if found) and passes it to function printCitation(index,para) which prints the citation number enclosed within square brackets. NOTE : Function printCitation(index,para) is recursively called in case of multiple citations.
