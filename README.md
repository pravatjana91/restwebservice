package pravat12.a;

import java.io.File;
import java.io.IOException;
import java.io.StringWriter;
import java.util.List;

import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;
import javax.xml.bind.Unmarshaller;
import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.bind.annotation.XmlRootElement;


import lombok.Data;

public class AbcV1 {

	public static void main(String args[]) throws  IOException, JAXBException {

        String filePath="C:\\Users\\prava\\OneDrive\\Desktop\\library-document.xml";
		JAXBContext jaxbContext = JAXBContext.newInstance(Gsafeed.class);

		Unmarshaller jaxbUnmarshaller = jaxbContext.createUnmarshaller();

		File file = new File(filePath);
		Gsafeed value = (Gsafeed) jaxbUnmarshaller.unmarshal(file);

		Marshaller marshaller = JAXBContext.newInstance(Gsafeed.class).createMarshaller();
		marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);

		StringWriter stringWriter = new StringWriter();

		marshaller.marshal(value, stringWriter);
		System.out.println(stringWriter);

	}
}

@Data
@XmlRootElement
class Gsafeed {
	
	@Data
	public static class Header {

		public String datasource;
		public String feedtype;
	}

	public Header header;
	public Group group;

	@Data

	public static class Group {

		public List<Record> record;

		@Data
		public static class Record {

			@XmlElement
			public Metadata metadata;

			@XmlAttribute
			public String url;

			@XmlAttribute
			public String mimetype;

			@XmlAttribute
			public String action;

			@Data
			public static class Metadata {

				@Data
				public static class Meta {
					@XmlAttribute

					public String name;

					@XmlAttribute
					public String content;
				}

				public List<Meta> meta;
			}

		}

	}

}
