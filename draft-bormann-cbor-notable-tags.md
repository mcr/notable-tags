---
title: >
  Notable CBOR Tags
abbrev: Notable CBOR Tags
docname: draft-bormann-cbor-notable-tags-latest
# date: 2021-02-12

stand_alone: true

ipr: trust200902
keyword: Internet-Draft
cat: info

pi: [toc, sortrefs, symrefs, compact, comments]

author:
  - name: Carsten Bormann
    org: Universität Bremen TZI
    street: Postfach 330440
    city: Bremen
    code: D-28359
    country: Germany
    phone: +49-421-218-63921
    email: cabo@tzi.org
contributor:
  - name: Peter Occil
    email: poccil14 at gmail dot com
    contribution: |
      Peter Occil registered tags 30, 264, 265, 268–270
      ({{advanced-arithmetic}}), 38, 257, 266 and 267
      ({{domain-specific}}), and contributed much of the text about
      these tags in this document.
  - name: Jane Doe
    org: To do
    contribution: |
      Further contributors will be listed here as text is added.

      Plase stay tuned.
normative:
  RFC8949: bis
  IANA.cbor-tags: tags
  RFC8610: cddl

informative:
  RFC2045: mime
  RFC4122: uuid
  RFC7049: orig
  RFC8742: seq
  I-D.bormann-cbor-time-tag: time-tag
--- abstract

The Concise Binary Object Representation (CBOR, RFC 7049) is a data
format whose design goals include the possibility of extremely small
code size, fairly small message size, and extensibility without the
need for version negotiation.

In CBOR, one point of extensibility is the definition of CBOR tags.
RFC 7049 and its revision 7049bis define a basic set of tags as well
as a registry that can be used to contribute additional tag
definitions {{-tags}}.  Since RFC 7049 was published, some 80 tag
definitions have been added to that registry.

The present document provides a roadmap to a large subset of these tag
definitions.  Where applicable, it points to a IETF standards or
standard development document
that specifies the tag.  Where no such document exists, the intention
is to collect specification information from the sources of the
registrations.  After some more development, the present document is
intended to be useful as a reference document for the IANA
registrations of the CBOR tags the definitions of which have been
collected.

--- note_Note_to_Readers

This is an individual submission to the CBOR working group of the
IETF, <https://datatracker.ietf.org/wg/cbor/about/>.
Discussion currently takes places on the github repository
<https://github.com/cabo/notable-tags>.
If the CBOR WG believes this is a useful document, discussion is
likely to move to the CBOR WG mailing list and a github repository at
the CBOR WG github organization, <https://github.com/cbor-wg>.

The current version is true work in progress; some of the sections
haven't been filled in yet, and in particular, permission has not been
obtained from tag definition authors to copy over their text.


--- middle

Introduction        {#intro}
============

(TO DO, expand on text from abstract here; move references here and
neuter them in the abstract as per Section 4.3 of {{?RFC7322}}.)

The selection of the tags presented here is somewhat arbitrary;
considerations such as how wide the scope and area of application of a
tag definition is combine with an assessment how "ready to use" the
tag definition is (i.e., is the tag specification in a state where it
can be used).

This document can only be a snapshot of a subset of the current registrations.
The most up to date set of registrations is always available in the registry at {{-tags}}.


Terminology         {#terms}
------------

The definitions of {{-bis}} apply.
The term "byte" is used in its now customary sense as a synonym for
"octet".
Where bit arithmetic is explained, this document uses the notation
familiar from the programming language C (including C++14's 0bnnn
binary literals), except that the operator "\*\*" stands for
exponentiation.

# RFC 7049 (CBOR)

{{-orig}} defines a number of tags that are listed here for
convenience only.

| Tag number | Tag content  | Short Description                         | Section of RFC 7049 |
|          0 | UTF-8 string | Standard date/time string                 |               2.4.1 |
|          1 | multiple     | Epoch-based date/time                     |               2.4.1 |
|          2 | byte string  | Positive bignum                           |               2.4.2 |
|          3 | byte string  | Negative bignum                           |               2.4.2 |
|          4 | array        | Decimal fraction                          |               2.4.3 |
|          5 | array        | Bigfloat                                  |               2.4.3 |
|         21 | multiple     | Expected conversion to base64url encoding |             2.4.4.2 |
|         22 | multiple     | Expected conversion to base64 encoding    |             2.4.4.2 |
|         23 | multiple     | Expected conversion to base16 encoding    |             2.4.4.2 |
|         24 | byte string  | Encoded CBOR data item                    |             2.4.4.1 |
|         32 | UTF-8 string | URI                                       |             2.4.4.3 |
|         33 | UTF-8 string | base64url                                 |             2.4.4.3 |
|         34 | UTF-8 string | base64                                    |             2.4.4.3 |
|         35 | UTF-8 string | Regular expression                        |             2.4.4.3 |
|         36 | UTF-8 string | MIME message                              |             2.4.4.3 |
|      55799 | multiple     | Self-describe CBOR                        |               2.4.5 |
{: #origtags title="Tag numbers defined in RFC 7049"}

## Tags Related to Those Defined in RFC 7049 {#related-tags}

Separately registered tags that are directly related to the tags
predefined in RFC 7049 include:

* Tag 63, registered by this document, is a parallel to tag 24, with
  the single difference that its byte string tag content carries a
  CBOR Sequence {{-seq}} instead of a single CBOR data items.

* Tag 257, registered by Peter Occil with a specification in
  <http://peteroupc.github.io/CBOR/binarymime.html>, is a parallel to
  tag 36, except that the tag content is a byte string, which
  therefore can also carry binary MIME messages as per {{-mime}}.

# Security

A number of CBOR tags are defined in security specifications that make
use of CBOR.

## RFC 8152 (COSE)

{{!RFC8152}} defines CBOR Object Signing and Encryption (COSE).
A revision is in process that splits this specification into the data
structure definitions {{?I-D.ietf-cose-rfc8152bis-struct}}, which will
define another tag for COSE standalone counter signature, and the
algorithms employed {{?I-D.ietf-cose-rfc8152bis-algs}}.

| Tag number | Tag content   | Short Description                           |
|         16 | COSE_Encrypt0 | COSE Single Recipient Encrypted Data Object |
|         17 | COSE_Mac0     | COSE Mac w/o Recipients Object              |
|         18 | COSE_Sign1    | COSE Single Signer Data Object              |
|         96 | COSE_Encrypt  | COSE Encrypted Data Object                  |
|         97 | COSE_Mac      | COSE MACed Data Object                      |
|         98 | COSE_Sign     | COSE Signed Data Object                     |
{: #cosetags title="Tag numbers defined in RFC 8152, COSE"}

## RFC 8392 (CWT)

{{!RFC8392}} defines the CBOR Web Token (CWT), making use of COSE to
define a CBOR variant of the JOSE Web Token (JWT), {{?RFC7519}}, a
standardized security token that has found use in the area of web
applications, but is not technically limited to those.

| Tag number | Tag content          | Short Description    |
|         61 | CBOR Web Token (CWT) | CBOR Web Token (CWT) |
{: #cwttags title="Tag number defined for RFC 8392 CBOR Web Token (CWT)"}

# CBOR-based Representation Formats

Representation formats can be built on top of CBOR.

## YANG-CBOR

YANG {{?RFC7950}} is a data modeling language originally designed in
the context of the Network Configuration Protocol (NETCONF)
{{?RFC6241}}, now widely used for modeling management and
configuration information.  {{?RFC7950}} defines an XML-based
representation format, and {{?RFC7951}} defines a JSON-based
{{?RFC8259}} representation format for YANG.

YANG-CBOR {{!I-D.ietf-core-yang-cbor}} is a representation format for
YANG data in CBOR.

| Tag number | Tag content                              | Short Description                 | Section of YANG-CBOR |
|         43 | byte string                              | YANG bits datatype                |                  6.7 |
|         44 | unsigned integer                         | YANG enumeration datatype         |                  6.6 |
|         45 | unsigned integer or text string          | YANG identityref datatype         |                 6.10 |
|         46 | unsigned integer or text string or array | YANG instance-identifier datatype |                 6.13 |
|         47 | unsigned integer                         | YANG Schema Item iDentifier (sid) |                  3.2 |
{: #yangtags title="Tag number defined for YANG-CBOR"}

# Protocols

Protocols may want to allocate CBOR tag numbers to identify specific
protocol elements.

## DOTS

DDoS Open Threat Signaling (DOTS) defines tag number 271 for the DOTS
signal channel object in {{!RFC8782}}.

## RAINS

As an example for how experimental protocols can make use of CBOR tag
definitions, the RAINS (Another Internet Naming Service) Protocol
Specification defines tag number 15309736 for a RAINS Message
{{?I-D.trammell-rains-protocol}}.


# Datatypes

## Advanced arithmetic

A number of tags have been registered for arithmetic representations
beyond those built into CBOR and defined by tags in {{-orig}}.
These are all documented under `http://peteroupc.github.io/CBOR/`; the
last pathname component is given in {{arithtags}}.

(TO DO: Obtain permission to copy the definitions here.)

| Tag number | Tag content | Short Description                         | Reference     |
|         30 | array       | Rational number                           | rational.html |
|        264 | array       | Decimal fraction with arbitrary  exponent | bigfrac.html  |
|        265 | array       | Bigfloat with arbitrary exponent          | bigfrac.html  |
|        268 | array       | Extended decimal fraction                 | extended.html |
|        269 | array       | Extended bigfloat                         | extended.html |
|        270 | array       | Extended rational number                  | extended.html |
{: #arithtags title="Tags for advanced arithmetic"}

## Variants of undefined

`https://github.com/svaarala/cbor-specs/blob/master/cbor-absent-tag.rst`
defines tag 31 to be applied to the CBOR value Undefined (0xf7),
slightly modifying its semantics to stand for an absent value in a
CBOR Array.

(TO DO: Obtain permission to copy the definitions here.)

## Typed and Homogeneous Arrays

{{!RFC8746}} defines tags for various kinds of arrays.  A summary is
reproduced in {{arraytags}}.

| Tag  | Data Item            | Semantics                                      |
| 64   | byte string          | uint8 Typed Array                              |
| 65   | byte string          | uint16, big endian, Typed Array                |
| 66   | byte string          | uint32, big endian, Typed Array                |
| 67   | byte string          | uint64, big endian, Typed Array                |
| 68   | byte string          | uint8 Typed Array, clamped arithmetic          |
| 69   | byte string          | uint16, little endian, Typed Array             |
| 70   | byte string          | uint32, little endian, Typed Array             |
| 71   | byte string          | uint64, little endian, Typed Array             |
| 72   | byte string          | sint8 Typed Array                              |
| 73   | byte string          | sint16, big endian, Typed Array                |
| 74   | byte string          | sint32, big endian, Typed Array                |
| 75   | byte string          | sint64, big endian, Typed Array                |
| 76   | byte string          | (reserved)                                     |
| 77   | byte string          | sint16, little endian, Typed Array             |
| 78   | byte string          | sint32, little endian, Typed Array             |
| 79   | byte string          | sint64, little endian, Typed Array             |
| 80   | byte string          | IEEE 754 binary16, big endian, Typed Array     |
| 81   | byte string          | IEEE 754 binary32, big endian, Typed Array     |
| 82   | byte string          | IEEE 754 binary64, big endian, Typed Array     |
| 83   | byte string          | IEEE 754 binary128, big endian, Typed Array    |
| 84   | byte string          | IEEE 754 binary16, little endian, Typed Array  |
| 85   | byte string          | IEEE 754 binary32, little endian, Typed Array  |
| 86   | byte string          | IEEE 754 binary64, little endian, Typed Array  |
| 87   | byte string          | IEEE 754 binary128, little endian, Typed Array |
| 40   | array of two arrays* | Multi-dimensional Array, row-major order       |
| 1040 | array of two arrays* | Multi-dimensional Array, column-major order    |
| 41   | array                | Homogeneous Array                              |
{: #arraytags title="Tag numbers defined for Arrays"}
<!--  cols='r l l' -->

# Domain-Specific


(TO DO: Obtain permission to copy the definitions here; create proper table.)


~~~
37                            byte string   Binary UUID ([RFC4122] section    [https://github.com/lucas-clemente/cbor-specs/blob/master/uuid.md][Lucas_Clemente]
                                            4.1.2)
38                            array         Language-tagged string            [http://peteroupc.github.io/CBOR/langtags.html][Peter_Occil]
257                           byte string   Binary MIME message               [http://peteroupc.github.io/CBOR/binarymime.html][Peter_Occil]


260                           byte string   Network Address (IPv4 or IPv6 or  [http://www.employees.org/~ravir/cbor-network.txt][Ravi_Raju]
                                            MAC Address)
                              map           Network Address Prefix (IPv4 or
261                           (IPAddress +  IPv6 Address + Mask Length)       [https://github.com/toravir/CBOR-Tag-Specs/blob/master/networkPrefix.md][Ravi_Raju]
                              Mask Length)

263                           byte string   Hexadecimal string                [https://github.com/toravir/CBOR-Tag-Specs/blob/master/hexString.md][Ravi_Raju]

266                           text string   Internationalized resource        [https://peteroupc.github.io/CBOR/iri.html][Peter_Occil]
                                            identifier (IRI)
                                            Internationalized resource
267                           text string   identifier reference (IRI         [https://peteroupc.github.io/CBOR/iri.html][Peter_Occil]
                                            reference)
~~~

## Extended Time Formats

Additional tag definitions have been provided for date and time values.

|  Tag | Data Item   | Semantics                          | Reference     |
|  100 | integer     | date in number of days since epoch | {{?RFC8943}}  |
| 1004 | text string | RFC 3339 full-date string          | {{?RFC8943}}  |
| 1001 | map         | extended time                      | {{-time-tag}} |
| 1002 | map         | duration                           | {{-time-tag}} |
| 1003 | map         | period                             | {{-time-tag}} |
{: #timetags cols='r l l' title="Tag numbers for date and time"}

Note that tags 100 and 1004 are for calendar dates that are not
anchored to a specific time zone; they are meant to specify calendar
dates as perceived by humans, e.g. for use in personal identification
documents.
Converting such a calendar date into a specific point in time needs the
addition of a time-of-day (for which a CBOR tag is outstanding) and
timezone information (also outstanding).  Alternatively, a calendar
date plus timezone information can be converted into a time period
(range of time values given by the starting and the ending time); note
that these time periods are not always exactly 24 h (86400 s) long.

{{?RFC8943}} does not suggest CDDL {{-cddl}} type names for the two tags.
We suggest copying the definitions in {{time-tags-cddl}} into
application-specific CDDL as needed.

~~~ cddl
caldate = #6.100(int) ; calendar date as a number of days from 1970-01-01
tcaldate = #6.1004(tstr) ; calendar date as an RFC 3339 full-date string
~~~
{: #time-tags-cddl title="CDDL for calendar date tags (RFC8943)"}

Tag 1001 extends tag 1 by additional information (such as picosecond
resolution) and allows the use of Decimal and Bigfloat numbers for the
time.

# Platform-oriented

## Perl

(These are actually not as Perl-specific as the title of this section
suggests.  See also the penultimate paragraph of Section 3.4 of {{-bis}}.)

These are all documented under `http://cbor.schmorp.de/`; the
last pathname component is given in {{perltags}}.

(TO DO: Obtain permission to copy the definitions here.)


|   Tag | Data Item        | Semantics                                                                       | Reference      |
|   256 | multiple         | mark value as having string references                                          | stringref      |
|    25 | unsigned integer | reference the nth previously seen string                                        | stringref      |
|    26 | array            | Serialised Perl object with classname and constructor arguments                 | perl-object    |
|    27 | array            | Serialised language-independent object with type name and constructor arguments | generic-object |
|    28 | multiple         | mark value as (potentially) shared                                              | value-sharing  |
|    29 | unsigned integer | reference nth marked value                                                      | value-sharing  |
| 22098 | multiple         | hint that indicates an additional level of indirection                          | indirection    |
{: #perltags cols='r l l' title="Tag numbers that aid the Perl platform"}


## JSON

(TO DO: Obtain permission to copy the definitions here.)


Tag number 262 has been registered to identify byte strings that carry embedded
JSON text (`https://github.com/toravir/CBOR-Tag-Specs/blob/master/embeddedJSON.md`).

Tag number 275 can be used to identify maps that contain keys that are
all of type Text String, as they would occur in JSON
(`https://github.com/ecorm/cbor-tag-text-key-map`).

## Weird text encodings

(TO DO: Obtain permission to copy the definitions here.)


Some variants of UTF-8 are in use in specific areas of application.
Tags have been registered to be able to carry around strings in these
variants in case they are not also valid UTF-8 and can therefore not
be represented as a CBOR text string
(`https://github.com/svaarala/cbor-specs/blob/master/cbor-nonutf8-string-tags.rst`).

| Tag Number | Data Item   | Semantics               |
|        272 | byte string | Non-UTF-8 CESU-8 string |
|        273 | byte string | Non-UTF-8 WTF-8 string  |
|        274 | byte string | Non-UTF-8 MUTF-8 string |
{: #weirdtags cols='r l l' title="Tag numbers for UTF-8 variants"}

# Application-specific

(TO DO: Obtain permission to copy the definitions here; create proper table.)


~~~
39                            multiple      Identifier                        [https://github.com/lucas-clemente/cbor-specs/blob/master/id.md][Lucas_Clemente]
42                            byte string   IPLD content identifier           [https://github.com/ipld/cid-cbor/][Volker_Mische]

103                           array         Geographic Coordinates            [https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag103-Geographic-Coordinates.md][Danilo_Vidovic]
104                           multiple      Geographic Coordinate Reference   [draft-clarke-cbor-crs]
                                            System WKT or EPSG number

120                           multiple      Internet of Things Data Point     [https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag120-Internet-of-Things-Data-Points.md][Danilo_Vidovic]



258                           array         Mathematical finite set           [https://github.com/input-output-hk/cbor-sets-spec/blob/master/CBOR_SETS.md][Alfredo_Di_Napoli]
                                            Map datatype with key-value
259                           map           operations (e.g.                  [https://github.com/shanewholloway/js-cbor-codec/blob/master/docs/CBOR-259-spec--explicit-maps.md][Shane_Holloway]
                                            `.get()/.set()/.delete()`)
~~~

# Implementation aids

## Invalid Tag

The present document registers tag numbers 65535, 4294967295, and
18446744073709551615 (16-bit 0xffff, 32-bit 0xffffffff, and 64-bit
0xffffffffffffffff) as Invalid Tags, tags that are always invalid,
independent of the tag content provided.  The purpose of these tag
number registrations is to enable the tag numbers to be reserved for
internal use by implementations to note the absence of a tag on a data
item where a tag could also be expected with that data item as tag
content.

The Invalid Tags are not intended to ever occur in interchanged CBOR
data items.  Generic CBOR decoder implementations are encouraged to
raise an error if an Invalid Tag occurs in a CBOR data item even if
there is no validity checking implemented otherwise.

IANA Considerations
============

In the registry {{-tags}},
IANA has allocated the first to third tag in {{tab-tag-values}} from the
FCFS space, with the present document as the specification reference.
IANA has allocated the fourth tag from the Specification
Required space, with the present document as the specification reference.

|                  Tag | Data Item    | Semantics                      | Reference                                         |
|                65535 | (none valid) | always invalid                 | draft-bormann-cbor-notable-tags, {{invalid-tag}}  |
|           4294967295 | (none valid) | always invalid                 | draft-bormann-cbor-notable-tags, {{invalid-tag}}  |
| 18446744073709551615 | (none valid) | always invalid                 | draft-bormann-cbor-notable-tags, {{invalid-tag}}  |
|                   63 | byte string  | Encoded CBOR Sequence {{-seq}} | draft-bormann-cbor-notable-tags, {{related-tags}} |
{: #tab-tag-values cols='r l l' title="Values for Tags"}

Security Considerations
============

The security considerations of {{-bis}} apply; the tags discussed here
may also have specific security considerations that are mentioned in
their specific sections above.

--- back

Acknowledgements
================
{: numbered="no"}

<!--  LocalWords:  CBOR extensibility IANA uint sint IEEE endian
 -->
<!--  LocalWords:  signedness endianness
 -->
