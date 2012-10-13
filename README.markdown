Grails Wkhtmltox / Wkhtmltopdf 
=========================

This plugin provides an easy integration of the wkthmltox library into grails.
http://code.google.com/p/wkhtmltopdf/

Installation
----------------

Mac
    brew install wkhtmltopdf

linux
    apt-get install wkhtmltopdf

see: http://code.google.com/p/wkhtmltopdf/wiki/compilation

Configuration
----------------

    grails.plugin.wkhtmltox.binary = "/usr/bin/wkhtmltopdf"


Usage
----------------

Now you can use the plugin, either stream the content of an action as pdf ( /context/some/someAction.pdf )

    class SomerController {
        def someAction = {
            def someInstance = SomeDomainObject.get(params.id)
    
            render( filename:"Rechnung ${someInstance.id}.pdf",
					view:"/some/someGspTemplate",
                    model:[someInstance:someInstance],
                    header:"/pdf/someHeader",
                    footer:"/pdf/someFooter",
                    marginLeft:20,
                    marginTop:35,
                    marginBottom:20,
                    marginRight:20,
                    headerSpacing:10,
            )
        }
    }

Or create binary pdf data and use them for any other purpose

    class SomeService implements Serializable {
    
    		def byte[] pdfData = wkhtmltoxService.makePdf(
                    view: "/pdf/someGspTemplate",
                    model: [someInstance: someInstance],
                    header: "/pdf/someHeader",
                    footer: "/pdf/someFooter",
                    marginLeft: 20,
                    marginTop: 35,
                    marginBottom: 20,
                    marginRight: 20,
                    headerSpacing: 10,
            )
    	
    	
    		// DO Something e.g. send as mail
    		//sendAsynchronousMail {
            //    multipart true
            //    to "mail@mail.de"
            //    subject "see PDF Attachment";
            //    attachBytes "PDF Attachment.pdf", "application/x-pdf", pdfData
            //    body "see my pdf attachment"
            //}
        }
    }