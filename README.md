package com.mycompany.mavenproject;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.dataformat.xml.XmlMapper;
import com.fasterxml.jackson.dataformat.xml.ser.ToXmlGenerator;
import java.io.File;
import java.io.IOException;
import java.io.StringWriter;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;
import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlValue;
import lombok.Data;

public class XmlToJavaToXml {

    public static void main(String args[]) throws JsonProcessingException, IOException, JAXBException {

        Path fileName = Path.of("C:\\Users\\prava\\OneDrive\\Desktop\\library-document.xml");
        String fileContent = Files.readString(fileName);

        XmlMapper xmlMapper = new XmlMapper();
        xmlMapper.configure(ToXmlGenerator.Feature.WRITE_XML_DECLARATION, true);

        Gsafeed value = xmlMapper.readValue(fileContent, Gsafeed.class);

             

        xmlMapper.writeValue(new File("C:\\Users\\prava\\OneDrive\\Desktop\\library-document_1.xml"), value);

    }
}

@Data
@XmlAccessorType(XmlAccessType.FIELD)

class Gsafeed {

    public Header header;
    public Group group;
}

@Data
class Header {
    @XmlAttribute

    public String datasource;
    @XmlAttribute

    public String feedtype;
}

@Data

class Meta {

    public String name;
    public String content;
}

@Data
class Metadata {

    public List<Meta> meta;
}

@Data

class Record {

    public Metadata metadata;

    @XmlAttribute
    public String url;

    @XmlAttribute
    public String mimetype;

        @XmlAttribute

    public String action;
}

@Data

class Group {

    public Record record;
}
