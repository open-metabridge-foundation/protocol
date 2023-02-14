# RFC draft

This folder contains the draft for the RFC. It can be written in markdown and later on be transformed into XML and TXT.

To convert markdown into XML, you can use [kramdown-rfc](https://github.com/cabo/kramdown-rfc):

    kramdown-rfc metabridge-protocol.md > metabridge-protocol.xml
    
To convert XML into ASCII TXT, you can use [xml2rfc](https://github.com/ietf-tools/xml2rfc):

    xml2rfc metabridge-protocol.xml

Alternatively, if you'd like to convert to HTML, use the following command:

    xml2rfc --html metabridge-protocol.xml