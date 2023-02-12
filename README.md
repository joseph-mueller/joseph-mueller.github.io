---
layout: default
---
# Documentation for the LXI API Spec Generation

This directory includes the LXI API schemas, and the tools used
to scrape the comments from them and into HTML for incorporation
into the LXI API Specification.

The official LXI copies of the schemas are in GitHub.  The GitHub
repository also has actions to build the html specification document
from the schemas. 

## Updating the API Extended Function Using GitHub

This section describes how to use GitHub and the GitHub actions
to update the LXI API schemas and the corresponding specification.
There is documentation in the README that describes the Python 
programs and batch files that are used to scrape the comments and
detailed information out of the schema files to create the html
file. 

----------------------------------------------

Follow these steps to create the API Extended Function 
Specification:

1. From MS Word: make any updates to the specification prose.

2. From MS Word: Update the Revision table, publication date, and 
   Version.

3. Clone the lxi-api repository, then from a Schema Editor 
  (such as Microsoft Visual Studio Code) incorporate 
  any necesssary changes to the schema or its 
  documentation into the appropriate sections of the schema files 
  (.xsd).  One easy way to do this is to edit the
  Extended Function specification in MS Word with change tracking 
  on.  This version can then be reviewed as a draft, then when stable
  resolve each change by incorporating the changes made in MS 
  Word into the schemas.

  **Remember to update the editorial date of any schema that is changed.**

  The Python used to generate the HTML (*buildSpec.py*)
  has the initial section and subsection so that it 
  calculates rule numbers that match the MS Word count.

  At the time of this writing, the section is 23 for the entire
  API Extended Function document, and subsection 11 is the last 
  level 2 header used before the beginning of the schema sections.  
  These two value must be entered in the buildSpec.py python 
  program.  For instance:

~~~
  specificationChapter = 23
  specificationLastTemplateSection = 11
~~~

  Once the schemas are pushed back to the GitHub
  repository, actions will run automatically to generate the html.  
  If the actions fail, look for syntax errors
  in the schemas.  Any errors should be resolved before moving on.

  The steps after this and before may be followed identically if the
  spec.html file is generated from the command line as described below.


4. At this point, the schemas in the repo have been updates and the 
  GitHub actions have build the html for the specification.

  To acquire the html file generated in GitHub (although the GUI
  could easily change, the following steps work August 2022):
  - Go to http://github.com/LxiStandard.
  - Click on the lxi-api repository
  - Click on the Actions tab near the top of the repository root page
  - Click on the most recent build
  - Click on the file to download
  - A zip file with a uniquified name shows up in your downloads with the new html
  

5.	Open the draft version of the MS Word specification.  Turn 
  off change tracking if it is enabled at this 
  point.

6.	From MS Word: Delete the sections in the draft spec that 
  will be replaced by the sections scraped from the schemas.  At 
  the time of this writing that is all sections from *LXI* *Common* 
  *Configuration* through the end.  This should be the sections 
  starting **immediately** **after** the 
  *specificationLastTemplateSection* indicated to Python above, 
  through the end. 

  - At the time of this writing, you delete from section 23.12 
    through the end.

7. From MS Word: insert the generated HTML in place of the 
  deleted text. The following steps work with the MS Word revision 
  current at the time of this writing: 

  - Navigate to the Insert toolbar and under *Object* select 
    *Insert* *Text* *from* *File*.  Insert the generated HTML at the 
    appropiate section.

8. From MS Word: add spacing between all of the generated 
  paragraphs (unless the MSWord HTML import has changed to not need 
  it).  To do so:

  - Select all of the text inserted from the HTML.
   
  - Navigate to the paragraph dialog (this is the dialog used to
    change various paragraph formatting parameters).
  
  - In the paragraph dialog, locate the section *Spacing*.  Then, under 
    *After* select 6 points. Apply the change.

9. From MS Word: Regenerate the Table of Contents and other field
  codes.  One way to do this is to: 1) Select the entire document (Ctrl-A), 
  and then 2) regenerate all field codes by pressing F9.  If prompted, 
  select “Update Entire Table” to properly update the Table of Contents.

10. Re-enable change tracking if desired.

11. Save the new spec, using whatever spec management processes are 
    appropriate.
    
12. Tag the lxi-api repo indicating the revision and editorial date.



# Customizing the generation of the spec.html

  The HTML generation works under both Linux and Windows.
  If either the chapter number for the lxi-api spec is changed or
  additional sections are added before the generated code is inserted
  the Python code has to be updated so it can generated appropriate
  cross references.

  The Python used to generate the HTML (*buildSpec.py*)
  has the initial section and subsection so that it 
  calculates rule numbers that match the MW Word count as described 
  in the following bullets.

  At the time of this writing, the section is 23 for the entire
  API Extended Function document, and subsection 11 is the last 
  level 2 header used before the beginning of the schema sections.  
  These two value must be entered in the buildSpec.py python 
  program.  For instance:

~~~
  specificationChapter = 23
  specificationLastTemplateSection = 11
~~~

  In addition, the Python used to generate the HTML (*buildSpec.py*) 
  may be configured to generate the MS Word insertion HTML or a 
  stand-alone HTML document.  This is controlled by a Boolean 
  in the Python generation script.

  Additional detail on the customerization and function of the 
  Python programs is included in-line in the Python programs. 

# Generating the HTML from the command shell

  As noted above, the HTML may be generated from either Linux
  or Windows. The script genHtml runs the high level steps to do so.
  There is a Windows bat file (*genHtml.bat*) and a Linux ksh file
  (*genHtml.sh*). Following this process is probably helpful if
  debugging or enhancing the HTML generation.

  Follow the documentation in the bullets  
  below to generate the HTML for the schema sections of the 
  specification:

  Ensure that the Python used to generate the HTML (*buildSpec.py*)
  has the appropriate initial section and subsection so that it 
  calculates rule numbers that match the MW Word count as described 
  in the following bullets.  See section above regarding updating
  the section numbers.
  
  Generate the HTML to insert into the spec by running genHtml.
  There is a Windows bat file (*genHtml.bat*) and a Linux ksh file
  (*genHtml.sh*).  These batch files generate HTML for the individual
  schemas as well at the HTML for the overall spec prose.


## Updating the API Extended Function Specification Manually
Before updating the MS Word specification, you should generate the
new HTML based on the schemas.  The primary tool to do this in 
genhtml.  This script (available in BAT and KSH) applies the
XSLT template to the schemas and generates HTML.  In addition it 
does various text processing required for the LXI specifications.

For detailed steps, see below.

The following code files are used:
- **genhtml.bat** and **genhtml.sh** (the highest level scripts to 
  just generate the documentation)
- **buildSpec.py** - Python program that does the work, just 
  invoked by genhtml.
- **LXISettingsTemplate.xsl** - The xslt used to generate HTML from 
  XSD
- **ApplyTepmplate.py** - This program just applies a 
  template to an XML file.  It is not used by buildSpec.py.

These files have conventional in-line documentation.


# Annotation XML used in the schemas

The XSD schemas include tags for annotation.  XSD provides a
free-format *appinfo* element with the *annotation* element.  The LXI
schemas use this to specify additional LXI information.

The LXI Schemas define three elements within 
xs:attribute/xs:annotation/xs:appinfo to simplify the entry and 
management of LXI specification information. They are:

- **requirement** Indicates the requirements around implementing 
this  attribute.  In numerous cases, this merely has a rule 
citation which indicate this attribute must be implemented.
- **lci** Indicates the LCI (LAN Connection Initialize) setting of 
this attribute.
- **unsecureMode** Indicates the impact of this attribute on 
unsecure mode.

Within these elements, general XHTML is accepted for detailed 
explanation.

# Editorial Date of the Schema

In addition to the information above, each schema has an 
editorial date.  The editorial date appears in the root element
of the schema at:

 **xs:schema/xs:element/xs:annotation/xs:appinfo/xs:editorialdate** 

This field nust be updated for each editorial release of the schema.

# Modifying the Code Generation

The *buildSpec.py* script has facilities to tune the spec generation
process.   Details of how to use them are in-line in the script.  The
following types of changes can be easily made:

- Add or remove schemas to the generated list.  This is especially
  useful if a schema is replaced with an updated version.
- Controlling the chapter and section numbering of the generated code
  to align with the MS Word chapter and section numbers.
- Add or manage "rule namespaces".  For instance, disjoint rule 
  numbering for rules such as "RULE(1.1):".
