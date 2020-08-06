.. _chapter_B:

Interface Definitions
=====================

.. _sect_B.1:

Application Interface - Version 20100825
----------------------------------------

.. _sect_B.1.1:

WSDL Definition of the Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following is the content of ApplicationService-20100825.wsdl:

::

   <?xml version="1.0" encoding="utf-8"?>
   <wsdl:definitions name="ApplicationService-20100825"
   targetNamespace="http://dicom.nema.org/PS3.19/ApplicationService-20100825"
   xmlns:tns="http://dicom.nema.org/PS3.19/ApplicationService-20100825"
   xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
   xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd"
   xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"
   xmlns:wsam="http://www.w3.org/2007/05/addressing/metadata"
   xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
   xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy"
   xmlns:wsap="http://schemas.xmlsoap.org/ws/2004/08/addressing/policy"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema"
   xmlns:msc="http://schemas.microsoft.com/ws/2005/12/wsdl/contract"
   xmlns:wsaw="http://www.w3.org/2006/05/addressing/wsdl"
   xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/"
   xmlns:wsa10="http://www.w3.org/2005/08/addressing"
   xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex"
   xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">
     <wsdl:types>
       <xsd:schema targetNamespace="http://dicom.nema.org/PS3.19/Imports/ApplicationService-20100825">

         <xsd:import namespace="http://dicom.nema.org/PS3.19/ApplicationService-20100825"
         schemaLocation="./ApplicationService-20100825.xsd" />
         <xsd:import namespace="http://schemas.microsoft.com/2003/10/Serialization/"
         schemaLocation="./Types.xsd" />
         <xsd:import namespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
         schemaLocation="./ArrayOfString.xsd" />
         <xsd:import namespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         schemaLocation="./XPathNodeType.xsd" />
       </xsd:schema>
     </wsdl:types>
     <wsdl:message name="IApplicationService_GetState_InputMessage">
       <wsdl:part name="parameters" element="tns:GetState" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_GetState_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetStateResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_SetState_InputMessage">
       <wsdl:part name="parameters" element="tns:SetState" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_SetState_OutputMessage">
       <wsdl:part name="parameters" element="tns:SetStateResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_BringToFront_InputMessage">
       <wsdl:part name="parameters" element="tns:BringToFront" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_BringToFront_OutputMessage">
       <wsdl:part name="parameters" element="tns:BringToFrontResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_NotifyDataAvailable_InputMessage">
       <wsdl:part name="parameters" element="tns:NotifyDataAvailable" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_NotifyDataAvailable_OutputMessage">
       <wsdl:part name="parameters" element="tns:NotifyDataAvailableResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_GetData_InputMessage">
       <wsdl:part name="parameters" element="tns:GetData" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_GetData_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetDataResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_ReleaseData_InputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseData" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_ReleaseData_OutputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseDataResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_GetAsModels_InputMessage">
       <wsdl:part name="parameters" element="tns:GetAsModels" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_GetAsModels_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetAsModelsResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_ReleaseModels_InputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseModels" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_ReleaseModels_OutputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseModelsResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_QueryModel_InputMessage">
       <wsdl:part name="parameters" element="tns:QueryModel" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_QueryModel_OutputMessage">
       <wsdl:part name="parameters" element="tns:QueryModelResponse" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_QueryInfoSet_InputMessage">
       <wsdl:part name="parameters" element="tns:QueryInfoSet" />
     </wsdl:message>
     <wsdl:message name="IApplicationService_QueryInfoSet_OutputMessage">
       <wsdl:part name="parameters" element="tns:QueryInfoSetResponse" />
     </wsdl:message>
     <wsdl:portType name="IApplicationService-20100825">
       <wsdl:operation name="GetState">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetState"
         message="tns:IApplicationService_GetState_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetStateResponse"
         message="tns:IApplicationService_GetState_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="SetState">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/SetState"
         message="tns:IApplicationService_SetState_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/SetStateResponse"
         message="tns:IApplicationService_SetState_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="BringToFront">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/BringToFront"
         message="tns:IApplicationService_BringToFront_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/BringToFrontResponse"
         message="tns:IApplicationService_BringToFront_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="NotifyDataAvailable">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/NotifyDataAvailable"
         message="tns:IApplicationService_NotifyDataAvailable_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/NotifyDataAvailableResponse"
         message="tns:IApplicationService_NotifyDataAvailable_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetData">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetData"
         message="tns:IApplicationService_GetData_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetDataResponse"
         message="tns:IApplicationService_GetData_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="ReleaseData">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseData"
         message="tns:IApplicationService_ReleaseData_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseDataResponse"
         message="tns:IApplicationService_ReleaseData_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetAsModels">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetAsModels"
         message="tns:IApplicationService_GetAsModels_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/GetAsModelsResponse"
         message="tns:IApplicationService_GetAsModels_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="ReleaseModels">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseModels"
         message="tns:IApplicationService_ReleaseModels_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseModelsResponse"
         message="tns:IApplicationService_ReleaseModels_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="QueryModel">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/QueryModel"
         message="tns:IApplicationService_QueryModel_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/QueryModelResponse"
         message="tns:IApplicationService_QueryModel_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="QueryInfoSet">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/QueryInfoSet"
         message="tns:IApplicationService_QueryInfoSet_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IApplicationService/QueryInfoSetResponse"
         message="tns:IApplicationService_QueryInfoSet_OutputMessage" />
       </wsdl:operation>
     </wsdl:portType>
     <wsdl:binding name="ApplicationService-20100825Binding"
     type="tns:IApplicationService-20100825">
       <soap:binding transport="http://schemas.xmlsoap.org/soap/http" />
       <wsdl:operation name="GetState">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/GetState"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="SetState">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/SetState"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="BringToFront">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/BringToFront"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="NotifyDataAvailable">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/NotifyDataAvailable"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetData">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/GetData"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="ReleaseData">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseData"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetAsModels">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/GetAsModels"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="ReleaseModels">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/ReleaseModels"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="QueryModel">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/QueryModel"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="QueryInfoSet">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IApplicationService/QueryInfoSet"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
     </wsdl:binding>
     <wsdl:service name="ApplicationService-20100825">
       <wsdl:port name="ApplicationServiceBinding"
       binding="tns:ApplicationService-20100825Binding">
         <soap:address location="http://localhost/Service" />
       </wsdl:port>
     </wsdl:service>
   </wsdl:definitions>

.. _sect_B.1.2:

Definition of Data Structures Used
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_B.1.2.1:

Primary Definitions
^^^^^^^^^^^^^^^^^^^

The following is the content of ApplicationService-20100825.xsd

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://dicom.nema.org/PS3.19/ApplicationService-20100825"
   elementFormDefault="qualified"
   targetNamespace="http://dicom.nema.org/PS3.19/ApplicationService-20100825"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays" />
     <xs:import namespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath" />
     <xs:element name="GetState">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="GetStateResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetStateResult" type="tns:State" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:simpleType name="State">
       <xs:restriction base="xs:string">
         <xs:enumeration value="IDLE" />
         <xs:enumeration value="INPROGRESS" />
         <xs:enumeration value="SUSPENDED" />
         <xs:enumeration value="COMPLETED" />
         <xs:enumeration value="CANCELED" />
         <xs:enumeration value="EXIT" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="State" nillable="true" type="tns:State" />
     <xs:element name="SetState">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="state" type="tns:State" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="SetStateResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="SetStateResult" type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="BringToFront">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="location" nillable="true"
           type="tns:Rectangle" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="Rectangle">
       <xs:sequence>
         <xs:element minOccurs="0" name="Height" type="xs:int" />
         <xs:element minOccurs="0" name="Width" type="xs:int" />
         <xs:element minOccurs="0" name="RefPointX" type="xs:int" />
         <xs:element minOccurs="0" name="RefPointY" type="xs:int" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Rectangle" nillable="true" type="tns:Rectangle" />
     <xs:element name="BringToFrontResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="BringToFrontResult"
           type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="NotifyDataAvailable">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="data" nillable="true"
           type="tns:AvailableData" />
           <xs:element minOccurs="0" name="lastData" type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="AvailableData">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Patients" nillable="true"
         type="tns:ArrayOfPatient" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="AvailableData" nillable="true" type="tns:AvailableData" />
     <xs:complexType name="ArrayOfObjectDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="ObjectDescriptor"
         nillable="true" type="tns:ObjectDescriptor" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfObjectDescriptor" nillable="true"
     type="tns:ArrayOfObjectDescriptor" />
     <xs:complexType name="ObjectDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" name="ClassUID" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="MimeType" nillable="true"
         type="tns:MimeType" />
         <xs:element minOccurs="0" name="Modality" nillable="true"
         type="tns:Modality" />
         <xs:element minOccurs="0" name="TransferSyntaxUID" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="DescriptorUuid" nillable="true"
         type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ObjectDescriptor" nillable="true"
     type="tns:ObjectDescriptor" />
     <xs:complexType name="UID">
       <xs:sequence>
         <xs:element minOccurs="0" name="Uid" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="UID" nillable="true" type="tns:UID" />
     <xs:complexType name="MimeType">
       <xs:sequence>
         <xs:element minOccurs="0" name="Type" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="MimeType" nillable="true" type="tns:MimeType" />
     <xs:complexType name="Modality">
       <xs:sequence>
         <xs:element minOccurs="0" name="Modality" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Modality" nillable="true" type="tns:Modality" />
     <xs:complexType name="UUID">
       <xs:sequence>
         <xs:element minOccurs="0" name="Uuid" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="UUID" nillable="true" type="tns:UUID" />
     <xs:complexType name="ArrayOfPatient">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Patient"
         nillable="true" type="tns:Patient" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfPatient" nillable="true"
     type="tns:ArrayOfPatient" />
     <xs:complexType name="Patient">
       <xs:sequence>
         <xs:element minOccurs="0" name="AssigningAuthority" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="DateOfBirth" type="xs:dateTime" />
         <xs:element minOccurs="0" name="ID" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="Name" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Sex" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="Studies" nillable="true"
         type="tns:ArrayOfStudy" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Patient" nillable="true" type="tns:Patient" />
     <xs:complexType name="ArrayOfStudy">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Study"
         nillable="true" type="tns:Study" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfStudy" nillable="true" type="tns:ArrayOfStudy" />
     <xs:complexType name="Study">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Series" nillable="true"
         type="tns:ArrayOfSeries" />
         <xs:element minOccurs="0" name="StudyUID" nillable="true"
         type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Study" nillable="true" type="tns:Study" />
     <xs:complexType name="ArrayOfSeries">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Series"
         nillable="true" type="tns:Series" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfSeries" nillable="true" type="tns:ArrayOfSeries" />
     <xs:complexType name="Series">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="SeriesUID" nillable="true"
         type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Series" nillable="true" type="tns:Series" />
     <xs:element name="NotifyDataAvailableResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="NotifyDataAvailableResult"
           type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="GetData">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="acceptableTransferSyntaxes"
           nillable="true" type="tns:ArrayOfUID" />
           <xs:element minOccurs="0" name="includeBulkData" type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfUUID">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="UUID"
         nillable="true" type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfUUID" nillable="true" type="tns:ArrayOfUUID" />
     <xs:complexType name="ArrayOfUID">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="UID"
         nillable="true" type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfUID" nillable="true" type="tns:ArrayOfUID" />
     <xs:element name="GetDataResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetDataResult" nillable="true"
           type="tns:ArrayOfObjectLocator" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfObjectLocator">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="ObjectLocator"
         nillable="true" type="tns:ObjectLocator" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfObjectLocator" nillable="true"
     type="tns:ArrayOfObjectLocator" />
     <xs:complexType name="ObjectLocator">
       <xs:sequence>
         <xs:element minOccurs="0" name="Length" type="xs:long" />
         <xs:element minOccurs="0" name="Offset" type="xs:long" />
         <xs:element minOccurs="0" name="TransferSyntax" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="URI" nillable="true" type="xs:anyURI" />
         <xs:element minOccurs="0" name="Locator" nillable="true"
         type="tns:UUID" />
         <xs:element minOccurs="0" name="Source" nillable="true"
         type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ObjectLocator" nillable="true" type="tns:ObjectLocator" />
     <xs:element name="ReleaseData">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="ReleaseDataResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="GetAsModels">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="classUID" nillable="true"
           type="tns:UID" />
           <xs:element minOccurs="0" name="supportedInfoSetTypes" nillable="true"
           type="tns:ArrayOfMimeType" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfMimeType">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="MimeType"
         nillable="true" type="tns:MimeType" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfMimeType" nillable="true"
     type="tns:ArrayOfMimeType" />
     <xs:element name="GetAsModelsResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetAsModelsResult" nillable="true"
           type="tns:ModelSetDescriptor" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ModelSetDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" name="FailedSourceObjects" nillable="true"
         type="tns:ArrayOfUUID" />
         <xs:element minOccurs="0" name="InfosetType" nillable="true"
         type="tns:MimeType" />
         <xs:element minOccurs="0" name="Models" nillable="true"
         type="tns:ArrayOfUUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ModelSetDescriptor" nillable="true"
     type="tns:ModelSetDescriptor" />
     <xs:element name="ReleaseModels">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="ReleaseModelsResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryModel">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="xPaths" nillable="true"
           xmlns:q1="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
           type="q1:ArrayOfstring" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryModelResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="QueryModelResult" nillable="true"
           type="tns:ArrayOfQueryResult" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfQueryResult">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="QueryResult"
         nillable="true" type="tns:QueryResult" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfQueryResult" nillable="true"
     type="tns:ArrayOfQueryResult" />
     <xs:complexType name="QueryResult">
       <xs:sequence>
         <xs:element minOccurs="0" name="Model" nillable="true" type="tns:UUID" />
         <xs:element minOccurs="0" name="Result" nillable="true"
         type="tns:ArrayOfXPathNode" />
         <xs:element minOccurs="0" name="XPath" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="QueryResult" nillable="true" type="tns:QueryResult" />
     <xs:complexType name="ArrayOfXPathNode">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="XPathNode"
         nillable="true" type="tns:XPathNode" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfXPathNode" nillable="true"
     type="tns:ArrayOfXPathNode" />
     <xs:complexType name="XPathNode">
       <xs:sequence>
         <xs:element minOccurs="0" name="NodeType"
         xmlns:q2="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         type="q2:XPathNodeType" />
         <xs:element minOccurs="0" name="Value" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="XPathNode" nillable="true" type="tns:XPathNode" />
     <xs:element name="QueryInfoSet">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="xPaths" nillable="true"
           xmlns:q3="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
           type="q3:ArrayOfstring" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryInfoSetResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="QueryInfoSetResult" nillable="true"
           type="tns:ArrayOfQueryResultInfoSet" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfQueryResultInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="QueryResultInfoSet"
         nillable="true" type="tns:QueryResultInfoSet" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfQueryResultInfoSet" nillable="true"
     type="tns:ArrayOfQueryResultInfoSet" />
     <xs:complexType name="QueryResultInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" name="Model" nillable="true" type="tns:UUID" />
         <xs:element minOccurs="0" name="Result" nillable="true"
         type="tns:ArrayOfXPathNodeInfoSet" />
         <xs:element minOccurs="0" name="XPath" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="QueryResultInfoSet" nillable="true"
     type="tns:QueryResultInfoSet" />
     <xs:complexType name="ArrayOfXPathNodeInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="XPathNodeInfoSet"
         nillable="true" type="tns:XPathNodeInfoSet" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfXPathNodeInfoSet" nillable="true"
     type="tns:ArrayOfXPathNodeInfoSet" />
     <xs:complexType name="XPathNodeInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" name="InfoSetValue" nillable="true"
         type="xs:base64Binary" />
         <xs:element minOccurs="0" name="NodeType"
         xmlns:q4="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         type="q4:XPathNodeType" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="XPathNodeInfoSet" nillable="true"
     type="tns:XPathNodeInfoSet" />
   </xs:schema>

.. _sect_B.1.2.2:

Referenced Definitions
^^^^^^^^^^^^^^^^^^^^^^

The following is the content of XPathNodeType.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
   elementFormDefault="qualified"
   targetNamespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:simpleType name="XPathNodeType">
       <xs:restriction base="xs:string">
         <xs:enumeration value="Root" />
         <xs:enumeration value="Element" />
         <xs:enumeration value="Attribute" />
         <xs:enumeration value="Namespace" />
         <xs:enumeration value="Text" />
         <xs:enumeration value="SignificantWhitespace" />
         <xs:enumeration value="Whitespace" />
         <xs:enumeration value="ProcessingInstruction" />
         <xs:enumeration value="Comment" />
         <xs:enumeration value="All" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="XPathNodeType" nillable="true" type="tns:XPathNodeType" />
   </xs:schema>

The following is the content of Types.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/"
   attributeFormDefault="qualified" elementFormDefault="qualified"
   targetNamespace="http://schemas.microsoft.com/2003/10/Serialization/"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:element name="anyType" nillable="true" type="xs:anyType" />
     <xs:element name="anyURI" nillable="true" type="xs:anyURI" />
     <xs:element name="base64Binary" nillable="true" type="xs:base64Binary" />
     <xs:element name="boolean" nillable="true" type="xs:boolean" />
     <xs:element name="byte" nillable="true" type="xs:byte" />
     <xs:element name="dateTime" nillable="true" type="xs:dateTime" />
     <xs:element name="decimal" nillable="true" type="xs:decimal" />
     <xs:element name="double" nillable="true" type="xs:double" />
     <xs:element name="float" nillable="true" type="xs:float" />
     <xs:element name="int" nillable="true" type="xs:int" />
     <xs:element name="long" nillable="true" type="xs:long" />
     <xs:element name="QName" nillable="true" type="xs:QName" />
     <xs:element name="short" nillable="true" type="xs:short" />
     <xs:element name="string" nillable="true" type="xs:string" />
     <xs:element name="unsignedByte" nillable="true" type="xs:unsignedByte" />
     <xs:element name="unsignedInt" nillable="true" type="xs:unsignedInt" />
     <xs:element name="unsignedLong" nillable="true" type="xs:unsignedLong" />
     <xs:element name="unsignedShort" nillable="true" type="xs:unsignedShort" />
     <xs:element name="char" nillable="true" type="tns:char" />
     <xs:simpleType name="char">
       <xs:restriction base="xs:int" />
     </xs:simpleType>
     <xs:element name="duration" nillable="true" type="tns:duration" />
     <xs:simpleType name="duration">
       <xs:restriction base="xs:duration">
         <xs:pattern value="\-?P(\d*D)?(T(\d*H)?(\d*M)?(\d*(\.\d*)?S)?)?" />
         <xs:minInclusive value="-P10675199DT2H48M5.4775808S" />
         <xs:maxInclusive value="P10675199DT2H48M5.4775807S" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="guid" nillable="true" type="tns:guid" />
     <xs:simpleType name="guid">
       <xs:restriction base="xs:string">
         <xs:pattern value="[\da-fA-F]{8}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{12}" />
       </xs:restriction>
     </xs:simpleType>
     <xs:attribute name="FactoryType" type="xs:QName" />
     <xs:attribute name="Id" type="xs:ID" />
     <xs:attribute name="Ref" type="xs:IDREF" />
   </xs:schema>

The following is the content of ArrayOfString.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
   elementFormDefault="qualified"
   targetNamespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:complexType name="ArrayOfstring">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="string"
         nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfstring" nillable="true" type="tns:ArrayOfstring" />
   </xs:schema>

.. _sect_B.2:

Host Interface - Version 20100825
---------------------------------

.. _sect_B.2.1:

WSDL Definition of the Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following is the content of HostService-20100825.wsdl:

::

   <?xml version="1.0" encoding="utf-8"?>
   <wsdl:definitions name="HostService-20100825"
   targetNamespace="http://dicom.nema.org/PS3.19/HostService-20100825"
   xmlns:tns="http://dicom.nema.org/PS3.19/HostService-20100825"
   xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
   xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd"
   xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"
   xmlns:wsam="http://www.w3.org/2007/05/addressing/metadata"
   xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
   xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy"
   xmlns:wsap="http://schemas.xmlsoap.org/ws/2004/08/addressing/policy"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema"
   xmlns:msc="http://schemas.microsoft.com/ws/2005/12/wsdl/contract"
   xmlns:wsaw="http://www.w3.org/2006/05/addressing/wsdl"
   xmlns:soap12="http://schemas.xmlsoap.org/wsdl/soap12/"
   xmlns:wsa10="http://www.w3.org/2005/08/addressing"
   xmlns:wsx="http://schemas.xmlsoap.org/ws/2004/09/mex"
   xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/">
     <wsdl:types>
       <xsd:schema targetNamespace="http://dicom.nema.org/PS3.19/Imports/HostService-20100825">

         <xsd:import namespace="http://dicom.nema.org/PS3.19/HostService-20100825"
         schemaLocation="./HostService-20100825.xsd" />
         <xsd:import namespace="http://schemas.microsoft.com/2003/10/Serialization/"
         schemaLocation="./Types.xsd" />
         <xsd:import namespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
         schemaLocation="./ArrayOfString.xsd" />
         <xsd:import namespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         schemaLocation="./XPathNodeType.xsd" />
       </xsd:schema>
     </wsdl:types>
     <wsdl:message name="IHostService_GenerateUID_InputMessage">
       <wsdl:part name="parameters" element="tns:GenerateUID" />
     </wsdl:message>
     <wsdl:message name="IHostService_GenerateUID_OutputMessage">
       <wsdl:part name="parameters" element="tns:GenerateUIDResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetAvailableScreen_InputMessage">
       <wsdl:part name="parameters" element="tns:GetAvailableScreen" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetAvailableScreen_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetAvailableScreenResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetOutputLocation_InputMessage">
       <wsdl:part name="parameters" element="tns:GetOutputLocation" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetOutputLocation_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetOutputLocationResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyStateChanged_InputMessage">
       <wsdl:part name="parameters" element="tns:NotifyStateChanged" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyStateChanged_OutputMessage">
       <wsdl:part name="parameters" element="tns:NotifyStateChangedResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyStatus_InputMessage">
       <wsdl:part name="parameters" element="tns:NotifyStatus" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyStatus_OutputMessage">
       <wsdl:part name="parameters" element="tns:NotifyStatusResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyDataAvailable_InputMessage">
       <wsdl:part name="parameters" element="tns:NotifyDataAvailable" />
     </wsdl:message>
     <wsdl:message name="IHostService_NotifyDataAvailable_OutputMessage">
       <wsdl:part name="parameters" element="tns:NotifyDataAvailableResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetData_InputMessage">
       <wsdl:part name="parameters" element="tns:GetData" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetData_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetDataResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_ReleaseData_InputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseData" />
     </wsdl:message>
     <wsdl:message name="IHostService_ReleaseData_OutputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseDataResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetAsModels_InputMessage">
       <wsdl:part name="parameters" element="tns:GetAsModels" />
     </wsdl:message>
     <wsdl:message name="IHostService_GetAsModels_OutputMessage">
       <wsdl:part name="parameters" element="tns:GetAsModelsResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_ReleaseModels_InputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseModels" />
     </wsdl:message>
     <wsdl:message name="IHostService_ReleaseModels_OutputMessage">
       <wsdl:part name="parameters" element="tns:ReleaseModelsResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_QueryModel_InputMessage">
       <wsdl:part name="parameters" element="tns:QueryModel" />
     </wsdl:message>
     <wsdl:message name="IHostService_QueryModel_OutputMessage">
       <wsdl:part name="parameters" element="tns:QueryModelResponse" />
     </wsdl:message>
     <wsdl:message name="IHostService_QueryInfoSet_InputMessage">
       <wsdl:part name="parameters" element="tns:QueryInfoSet" />
     </wsdl:message>
     <wsdl:message name="IHostService_QueryInfoSet_OutputMessage">
       <wsdl:part name="parameters" element="tns:QueryInfoSetResponse" />
     </wsdl:message>
     <wsdl:portType name="IHostService-20100825">
       <wsdl:operation name="GenerateUID">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GenerateUID"
         message="tns:IHostService_GenerateUID_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GenerateUIDResponse"
         message="tns:IHostService_GenerateUID_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetAvailableScreen">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetAvailableScreen"
         message="tns:IHostService_GetAvailableScreen_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetAvailableScreenResponse"
         message="tns:IHostService_GetAvailableScreen_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetOutputLocation">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetOutputLocation"
         message="tns:IHostService_GetOutputLocation_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetOutputLocationResponse"
         message="tns:IHostService_GetOutputLocation_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="NotifyStateChanged">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyStateChanged"
         message="tns:IHostService_NotifyStateChanged_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyStateChangedResponse"
         message="tns:IHostService_NotifyStateChanged_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="NotifyStatus">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyStatus"
         message="tns:IHostService_NotifyStatus_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyStatusResponse"
         message="tns:IHostService_NotifyStatus_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="NotifyDataAvailable">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyDataAvailable"
         message="tns:IHostService_NotifyDataAvailable_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/NotifyDataAvailableResponse"
         message="tns:IHostService_NotifyDataAvailable_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetData">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetData"
         message="tns:IHostService_GetData_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetDataResponse"
         message="tns:IHostService_GetData_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="ReleaseData">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/ReleaseData"
         message="tns:IHostService_ReleaseData_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/ReleaseDataResponse"
         message="tns:IHostService_ReleaseData_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="GetAsModels">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetAsModels"
         message="tns:IHostService_GetAsModels_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/GetAsModelsResponse"
         message="tns:IHostService_GetAsModels_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="ReleaseModels">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/ReleaseModels"
         message="tns:IHostService_ReleaseModels_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/ReleaseModelsResponse"
         message="tns:IHostService_ReleaseModels_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="QueryModel">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/QueryModel"
         message="tns:IHostService_QueryModel_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/QueryModelResponse"
         message="tns:IHostService_QueryModel_OutputMessage" />
       </wsdl:operation>
       <wsdl:operation name="QueryInfoSet">
         <wsdl:input wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/QueryInfoSet"
         message="tns:IHostService_QueryInfoSet_InputMessage" />
         <wsdl:output
           wsaw:Action="http://dicom.nema.org/PS3.19/IHostService/QueryInfoSetResponse"
         message="tns:IHostService_QueryInfoSet_OutputMessage" />
       </wsdl:operation>
     </wsdl:portType>
     <wsdl:binding name="HostService-YYYYNNDDBinding"
     type="tns:IHostService-20100825">
       <soap:binding transport="http://schemas.xmlsoap.org/soap/http" />
       <wsdl:operation name="GenerateUID">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/GenerateUID"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetAvailableScreen">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/GetAvailableScreen"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetOutputLocation">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/GetOutputLocation"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="NotifyStateChanged">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/NotifyStateChanged"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="NotifyStatus">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/NotifyStatus"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="NotifyDataAvailable">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/NotifyDataAvailable"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetData">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/GetData"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="ReleaseData">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/ReleaseData"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="GetAsModels">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/GetAsModels"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="ReleaseModels">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/ReleaseModels"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="QueryModel">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/QueryModel"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
       <wsdl:operation name="QueryInfoSet">
         <soap:operation
            soapAction="http://dicom.nema.org/PS3.19/IHostService/QueryInfoSet"
         style="document" />
         <wsdl:input>
           <soap:body use="literal" />
         </wsdl:input>
         <wsdl:output>
           <soap:body use="literal" />
         </wsdl:output>
       </wsdl:operation>
     </wsdl:binding>
     <wsdl:service name="HostService-20100825">
       <wsdl:port name="HostServiceBinding"
       binding="tns:HostService-YYYYNNDDBinding">
         <soap:address location="http://localhost/Service" />
       </wsdl:port>
     </wsdl:service>
   </wsdl:definitions>

.. _sect_B.2.2:

Definition of Data Structures Used
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _sect_B.2.2.1:

Primary Definitions
^^^^^^^^^^^^^^^^^^^

The following is the the contents of HostService-20100825.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://dicom.nema.org/PS3.19/HostService-20100825"
   elementFormDefault="qualified"
   targetNamespace="http://dicom.nema.org/PS3.19/HostService-20100825"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays" />
     <xs:import namespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath" />
     <xs:element name="GenerateUID">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="GenerateUIDResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GenerateUIDResult" nillable="true"
           type="tns:UID" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="UID">
       <xs:sequence>
         <xs:element minOccurs="0" name="Uid" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="UID" nillable="true" type="tns:UID" />
     <xs:element name="GetAvailableScreen">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="preferredScreen" nillable="true"
           type="tns:Rectangle" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="Rectangle">
       <xs:sequence>
         <xs:element minOccurs="0" name="Height" type="xs:int" />
         <xs:element minOccurs="0" name="Width" type="xs:int" />
         <xs:element minOccurs="0" name="RefPointX" type="xs:int" />
         <xs:element minOccurs="0" name="RefPointY" type="xs:int" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Rectangle" nillable="true" type="tns:Rectangle" />
     <xs:element name="GetAvailableScreenResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetAvailableScreenResult"
           nillable="true" type="tns:Rectangle" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="GetOutputLocation">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="preferredProtocols" nillable="true"
           xmlns:q1="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
           type="q1:ArrayOfstring" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="GetOutputLocationResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetOutputLocationResult"
           nillable="true" type="xs:anyURI" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="NotifyStateChanged">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="state" type="tns:State" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:simpleType name="State">
       <xs:restriction base="xs:string">
         <xs:enumeration value="IDLE" />
         <xs:enumeration value="INPROGRESS" />
         <xs:enumeration value="SUSPENDED" />
         <xs:enumeration value="COMPLETED" />
         <xs:enumeration value="CANCELED" />
         <xs:enumeration value="EXIT" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="State" nillable="true" type="tns:State" />
     <xs:element name="NotifyStateChangedResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="NotifyStatus">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="status" nillable="true"
           type="tns:Status" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="Status">
       <xs:sequence>
         <xs:element minOccurs="0" name="StatusType" type="tns:StatusType" />
         <xs:element minOccurs="0" name="CodeValue" type="xs:int" />
         <xs:element minOccurs="0" name="CodingSchemeDesignator" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="CodeMeaning" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="ContextIdentifier" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="MappingResource" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="ContextGroupVersion" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="ContextGroupExtensionFlag"
         nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="ContextGroupLocalVersion" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="ContextGroupExtensionCreatorUID"
         nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Status" nillable="true" type="tns:Status" />
     <xs:simpleType name="StatusType">
       <xs:restriction base="xs:string">
         <xs:enumeration value="INFORMATION" />
         <xs:enumeration value="WARNING" />
         <xs:enumeration value="ERROR" />
         <xs:enumeration value="FATALERROR" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="StatusType" nillable="true" type="tns:StatusType" />
     <xs:element name="NotifyStatusResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="NotifyDataAvailable">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="data" nillable="true"
           type="tns:AvailableData" />
           <xs:element minOccurs="0" name="lastData" type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="AvailableData">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Patients" nillable="true"
         type="tns:ArrayOfPatient" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="AvailableData" nillable="true" type="tns:AvailableData" />
     <xs:complexType name="ArrayOfObjectDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="ObjectDescriptor"
         nillable="true" type="tns:ObjectDescriptor" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfObjectDescriptor" nillable="true"
     type="tns:ArrayOfObjectDescriptor" />
     <xs:complexType name="ObjectDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" name="ClassUID" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="MimeType" nillable="true"
         type="tns:MimeType" />
         <xs:element minOccurs="0" name="Modality" nillable="true"
         type="tns:Modality" />
         <xs:element minOccurs="0" name="TransferSyntaxUID" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="DescriptorUuid" nillable="true"
         type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ObjectDescriptor" nillable="true"
     type="tns:ObjectDescriptor" />
     <xs:complexType name="MimeType">
       <xs:sequence>
         <xs:element minOccurs="0" name="Type" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="MimeType" nillable="true" type="tns:MimeType" />
     <xs:complexType name="Modality">
       <xs:sequence>
         <xs:element minOccurs="0" name="Modality" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Modality" nillable="true" type="tns:Modality" />
     <xs:complexType name="UUID">
       <xs:sequence>
         <xs:element minOccurs="0" name="Uuid" nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="UUID" nillable="true" type="tns:UUID" />
     <xs:complexType name="ArrayOfPatient">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Patient"
         nillable="true" type="tns:Patient" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfPatient" nillable="true"
     type="tns:ArrayOfPatient" />
     <xs:complexType name="Patient">
       <xs:sequence>
         <xs:element minOccurs="0" name="AssigningAuthority" nillable="true"
         type="xs:string" />
         <xs:element minOccurs="0" name="DateOfBirth" type="xs:dateTime" />
         <xs:element minOccurs="0" name="ID" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="Name" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Sex" nillable="true" type="xs:string" />
         <xs:element minOccurs="0" name="Studies" nillable="true"
         type="tns:ArrayOfStudy" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Patient" nillable="true" type="tns:Patient" />
     <xs:complexType name="ArrayOfStudy">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Study"
         nillable="true" type="tns:Study" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfStudy" nillable="true" type="tns:ArrayOfStudy" />
     <xs:complexType name="Study">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="Series" nillable="true"
         type="tns:ArrayOfSeries" />
         <xs:element minOccurs="0" name="StudyUID" nillable="true"
         type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Study" nillable="true" type="tns:Study" />
     <xs:complexType name="ArrayOfSeries">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="Series"
         nillable="true" type="tns:Series" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfSeries" nillable="true" type="tns:ArrayOfSeries" />
     <xs:complexType name="Series">
       <xs:sequence>
         <xs:element minOccurs="0" name="ObjectDescriptors" nillable="true"
         type="tns:ArrayOfObjectDescriptor" />
         <xs:element minOccurs="0" name="SeriesUID" nillable="true"
         type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="Series" nillable="true" type="tns:Series" />
     <xs:element name="NotifyDataAvailableResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="NotifyDataAvailableResult"
           type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="GetData">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="acceptableTransferSyntaxes"
           nillable="true" type="tns:ArrayOfUID" />
           <xs:element minOccurs="0" name="includeBulkData" type="xs:boolean" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfUUID">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="UUID"
         nillable="true" type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfUUID" nillable="true" type="tns:ArrayOfUUID" />
     <xs:complexType name="ArrayOfUID">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="UID"
         nillable="true" type="tns:UID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfUID" nillable="true" type="tns:ArrayOfUID" />
     <xs:element name="GetDataResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetDataResult" nillable="true"
           type="tns:ArrayOfObjectLocator" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfObjectLocator">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="ObjectLocator"
         nillable="true" type="tns:ObjectLocator" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfObjectLocator" nillable="true"
     type="tns:ArrayOfObjectLocator" />
     <xs:complexType name="ObjectLocator">
       <xs:sequence>
         <xs:element minOccurs="0" name="Length" type="xs:long" />
         <xs:element minOccurs="0" name="Offset" type="xs:long" />
         <xs:element minOccurs="0" name="TransferSyntax" nillable="true"
         type="tns:UID" />
         <xs:element minOccurs="0" name="URI" nillable="true" type="xs:anyURI" />
         <xs:element minOccurs="0" name="Locator" nillable="true"
         type="tns:UUID" />
         <xs:element minOccurs="0" name="Source" nillable="true"
         type="tns:UUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ObjectLocator" nillable="true" type="tns:ObjectLocator" />
     <xs:element name="ReleaseData">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="ReleaseDataResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="GetAsModels">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="objects" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="classUID" nillable="true"
           type="tns:UID" />
           <xs:element minOccurs="0" name="supportedInfoSetTypes" nillable="true"
           type="tns:ArrayOfMimeType" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfMimeType">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="MimeType"
         nillable="true" type="tns:MimeType" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfMimeType" nillable="true"
     type="tns:ArrayOfMimeType" />
     <xs:element name="GetAsModelsResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="GetAsModelsResult" nillable="true"
           type="tns:ModelSetDescriptor" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ModelSetDescriptor">
       <xs:sequence>
         <xs:element minOccurs="0" name="FailedSourceObjects" nillable="true"
         type="tns:ArrayOfUUID" />
         <xs:element minOccurs="0" name="InfosetType" nillable="true"
         type="tns:MimeType" />
         <xs:element minOccurs="0" name="Models" nillable="true"
         type="tns:ArrayOfUUID" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ModelSetDescriptor" nillable="true"
     type="tns:ModelSetDescriptor" />
     <xs:element name="ReleaseModels">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="ReleaseModelsResponse">
       <xs:complexType>
         <xs:sequence />
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryModel">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="xPaths" nillable="true"
           xmlns:q2="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
           type="q2:ArrayOfstring" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryModelResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="QueryModelResult" nillable="true"
           type="tns:ArrayOfQueryResult" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfQueryResult">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="QueryResult"
         nillable="true" type="tns:QueryResult" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfQueryResult" nillable="true"
     type="tns:ArrayOfQueryResult" />
     <xs:complexType name="QueryResult">
       <xs:sequence>
         <xs:element minOccurs="0" name="Model" nillable="true" type="tns:UUID" />
         <xs:element minOccurs="0" name="Result" nillable="true"
         type="tns:ArrayOfXPathNode" />
         <xs:element minOccurs="0" name="XPath" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="QueryResult" nillable="true" type="tns:QueryResult" />
     <xs:complexType name="ArrayOfXPathNode">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="XPathNode"
         nillable="true" type="tns:XPathNode" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfXPathNode" nillable="true"
     type="tns:ArrayOfXPathNode" />
     <xs:complexType name="XPathNode">
       <xs:sequence>
         <xs:element minOccurs="0" name="NodeType"
         xmlns:q3="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         type="q3:XPathNodeType" />
         <xs:element minOccurs="0" name="Value" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="XPathNode" nillable="true" type="tns:XPathNode" />
     <xs:element name="QueryInfoSet">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="models" nillable="true"
           type="tns:ArrayOfUUID" />
           <xs:element minOccurs="0" name="xPaths" nillable="true"
           xmlns:q4="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
           type="q4:ArrayOfstring" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:element name="QueryInfoSetResponse">
       <xs:complexType>
         <xs:sequence>
           <xs:element minOccurs="0" name="QueryInfoSetResult" nillable="true"
           type="tns:ArrayOfQueryResultInfoSet" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
     <xs:complexType name="ArrayOfQueryResultInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="QueryResultInfoSet"
         nillable="true" type="tns:QueryResultInfoSet" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfQueryResultInfoSet" nillable="true"
     type="tns:ArrayOfQueryResultInfoSet" />
     <xs:complexType name="QueryResultInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" name="Model" nillable="true" type="tns:UUID" />
         <xs:element minOccurs="0" name="Result" nillable="true"
         type="tns:ArrayOfXPathNodeInfoSet" />
         <xs:element minOccurs="0" name="XPath" nillable="true"
         type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="QueryResultInfoSet" nillable="true"
     type="tns:QueryResultInfoSet" />
     <xs:complexType name="ArrayOfXPathNodeInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="XPathNodeInfoSet"
         nillable="true" type="tns:XPathNodeInfoSet" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfXPathNodeInfoSet" nillable="true"
     type="tns:ArrayOfXPathNodeInfoSet" />
     <xs:complexType name="XPathNodeInfoSet">
       <xs:sequence>
         <xs:element minOccurs="0" name="InfoSetValue" nillable="true"
         type="xs:base64Binary" />
         <xs:element minOccurs="0" name="NodeType"
         xmlns:q5="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
         type="q5:XPathNodeType" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="XPathNodeInfoSet" nillable="true"
     type="tns:XPathNodeInfoSet" />
   </xs:schema>

.. _sect_B.2.2.2:

Referenced Definitions
^^^^^^^^^^^^^^^^^^^^^^

The following is the content of XPathNodeType.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
   elementFormDefault="qualified"
   targetNamespace="http://schemas.datacontract.org/2004/07/System.Xml.XPath"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:simpleType name="XPathNodeType">
       <xs:restriction base="xs:string">
         <xs:enumeration value="Root" />
         <xs:enumeration value="Element" />
         <xs:enumeration value="Attribute" />
         <xs:enumeration value="Namespace" />
         <xs:enumeration value="Text" />
         <xs:enumeration value="SignificantWhitespace" />
         <xs:enumeration value="Whitespace" />
         <xs:enumeration value="ProcessingInstruction" />
         <xs:enumeration value="Comment" />
         <xs:enumeration value="All" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="XPathNodeType" nillable="true" type="tns:XPathNodeType" />
   </xs:schema>

The following is the content of Types.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/"
   attributeFormDefault="qualified" elementFormDefault="qualified"
   targetNamespace="http://schemas.microsoft.com/2003/10/Serialization/"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:element name="anyType" nillable="true" type="xs:anyType" />
     <xs:element name="anyURI" nillable="true" type="xs:anyURI" />
     <xs:element name="base64Binary" nillable="true" type="xs:base64Binary" />
     <xs:element name="boolean" nillable="true" type="xs:boolean" />
     <xs:element name="byte" nillable="true" type="xs:byte" />
     <xs:element name="dateTime" nillable="true" type="xs:dateTime" />
     <xs:element name="decimal" nillable="true" type="xs:decimal" />
     <xs:element name="double" nillable="true" type="xs:double" />
     <xs:element name="float" nillable="true" type="xs:float" />
     <xs:element name="int" nillable="true" type="xs:int" />
     <xs:element name="long" nillable="true" type="xs:long" />
     <xs:element name="QName" nillable="true" type="xs:QName" />
     <xs:element name="short" nillable="true" type="xs:short" />
     <xs:element name="string" nillable="true" type="xs:string" />
     <xs:element name="unsignedByte" nillable="true" type="xs:unsignedByte" />
     <xs:element name="unsignedInt" nillable="true" type="xs:unsignedInt" />
     <xs:element name="unsignedLong" nillable="true" type="xs:unsignedLong" />
     <xs:element name="unsignedShort" nillable="true" type="xs:unsignedShort" />
     <xs:element name="char" nillable="true" type="tns:char" />
     <xs:simpleType name="char">
       <xs:restriction base="xs:int" />
     </xs:simpleType>
     <xs:element name="duration" nillable="true" type="tns:duration" />
     <xs:simpleType name="duration">
       <xs:restriction base="xs:duration">
         <xs:pattern value="\-?P(\d*D)?(T(\d*H)?(\d*M)?(\d*(\.\d*)?S)?)?" />
         <xs:minInclusive value="-P10675199DT2H48M5.4775808S" />
         <xs:maxInclusive value="P10675199DT2H48M5.4775807S" />
       </xs:restriction>
     </xs:simpleType>
     <xs:element name="guid" nillable="true" type="tns:guid" />
     <xs:simpleType name="guid">
       <xs:restriction base="xs:string">
         <xs:pattern value="[\da-fA-F]{8}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{12}" />
       </xs:restriction>
     </xs:simpleType>
     <xs:attribute name="FactoryType" type="xs:QName" />
     <xs:attribute name="Id" type="xs:ID" />
     <xs:attribute name="Ref" type="xs:IDREF" />
   </xs:schema>

The following is the content of ArrayOfString.xsd:

::

   <?xml version="1.0" encoding="utf-8"?>
   <xs:schema xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
   elementFormDefault="qualified"
   targetNamespace="http://schemas.microsoft.com/2003/10/Serialization/Arrays"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:complexType name="ArrayOfstring">
       <xs:sequence>
         <xs:element minOccurs="0" maxOccurs="unbounded" name="string"
         nillable="true" type="xs:string" />
       </xs:sequence>
     </xs:complexType>
     <xs:element name="ArrayOfstring" nillable="true" type="tns:ArrayOfstring" />
   </xs:schema>
