---
title: 以编程方式使用AEM文档服务
description: 了解如何使用Document Services API对文档进行数字签名、加密、标记和生成PDF文档。
feature: Document Services,APIs & Integrations
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 5c6fa5ae-ac28-4d92-9123-f4f1404bdc4f
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '6439'
ht-degree: 1%

---

# 以编程方式使用AEM文档服务  {#using-aem-document-services-programmatically}

本文档中的示例和示例可帮助您了解在OSGi环境上的AEM Forms上使用AEM Document Services 。 有关JEE环境上的AEM Forms的示例和示例，请参阅

* [签名服务Java API快速入门](/help/forms/developing/signature-service-java-api-quick.md#programming-aem-forms-jee)

* [加密服务Java API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#developer-reference)

* [Acrobat Reader扩展服务Java API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#developer-reference)

## 先决条件 {#prerequisite}

* 在使用DocAssurance服务API之前，[配置DocAssurance服务](/help/forms/using/install-configure-document-services.md)。

* 下载并使用AEM Forms maven项目配置[AEM客户端SDK](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)。 该网站上提供了使用AEM Document Services构建Maven项目所需的客户端类。

* 了解[如何使用Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)

## DocAssurance服务 {#docassurance-service}

DocAssurance服务包括以下服务：

* 签名服务
* 加密服务
* Reader扩展服务

您可以使用DocAssurance服务执行以下操作：

* [添加不可见签名](/help/forms/using/aem-document-services-programmatically.md#p-adding-an-invisible-signature-field-p)

* [添加签名字段](/help/forms/using/aem-document-services-programmatically.md#p-adding-a-signature-field-nbsp-p)
* [应用文档时间戳](/help/forms/using/aem-document-services-programmatically.md#apply-document-timestamp)

* [获取签名](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-p)
* [获取签名字段列表](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-field-list-nbsp-p)
* [修改签名字段](/help/forms/using/aem-document-services-programmatically.md#p-modifying-signature-fields-nbsp-p)

* [安全文档](/help/forms/using/aem-document-services-programmatically.md#p-securing-documents-p)

* [获取凭据使用权限](/help/forms/using/aem-document-services-programmatically.md#p-getting-credential-usage-rights-p)

* [获取文档使用权限](/help/forms/using/aem-document-services-programmatically.md#p-getting-document-usage-rights-p)

* [删除使用权限](/help/forms/using/aem-document-services-programmatically.md#p-removing-usage-rights-p)
* [验证数字签名](/help/forms/using/aem-document-services-programmatically.md#p-verifying-digital-signatures-p)
* [验证多个数字签名](/help/forms/using/aem-document-services-programmatically.md#p-verifying-multiple-digital-signatures-p)
* [删除数字签名](/help/forms/using/aem-document-services-programmatically.md#p-removing-digital-signatures-p)

* [获取认证签名字段](/help/forms/using/aem-document-services-programmatically.md#p-getting-certifying-signature-field-p)
* [获取PDF加密类型](/help/forms/using/aem-document-services-programmatically.md#p-getting-pdf-encryption-type-p)
* [删除密码加密](/help/forms/using/aem-document-services-programmatically.md#p-removing-password-encryption-from-pdf-p)

* [删除证书加密](/help/forms/using/aem-document-services-programmatically.md#p-removing-certificate-encryption-p)

>[!NOTE]
>
>所有这些服务都使用Document对象作为输入参数，可在URL [https://helpx.adobe.com/cn/experience-manager/6-3/forms/javadocs/index.html](https://helpx.adobe.com/cn/experience-manager/6-3/forms/javadocs/index.html)上找到该输入参数的Javadoc

### 添加不可见的签名字段 {#adding-an-invisible-signature-field}

数字签名出现在签名字段中，这些签名字段是包含签名的图形表示的表单字段。 签名字段可以是可见的或不可见的。 签名者可以使用预先存在的签名字段，也可以以编程方式添加签名字段。 在任一情况下，签名PDF文档之前必须存在签名字段。 您可以使用签名服务Java API或签名Web服务API以编程方式添加签名字段。 您可以向PDF文档添加多个签名字段。 但是，每个签名字段名称必须是唯一的。

**语法**： `addInvisibleSignatureField(Document inDoc, String signatureFieldName, FieldMDPOptionSpec fieldMDPOptionsSpec, PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF.<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code><br /> </td>
   <td>签名字段的名称。 此参数是必需的，不能有null作为值。<br /> </td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td><code>FieldMDPOptionSpec</code>对象，它指定签名字段后锁定的PDF文档字段。 此参数是可选的，可以接受null值。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>指定字段的各种种子值的<code>SeedValueOptions</code>对象。 T此参数是可选的，可以接受null值。<span class="acrolinxCursorMarker"></span></td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。只有加密文件才需要此参数。</td>
  </tr>
 </tbody>
</table>

以下是一个Java代码示例，用于向PDF文档添加不可见的签名字段。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds an invisible signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddInvisibleSignatureField.class)
public class AddInvisibleSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addInvisibleSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addInvisibleSignatureField(
       inDoc,
       fieldName,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

您还可以使用[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)规范对文档进行签名。 使用以下示例代码设置[CAdES.](https://en.wikipedia.org/wiki/CAdES_%28computing%29)的签名格式

```java
SigningFormat signingFormat = SigningFormat.CAdES;
sigAppearence.setSigningFormat(signingFormat);
signOptions.setSigAppearence(sigAppearence);
```

### 添加签名字段  {#adding-a-signature-field-nbsp}

您可以使用签名服务Java API或签名Web服务API以编程方式添加签名字段。 您可以将多个签名字段添加到PDF文档中。 但是，每个签名字段名称必须是唯一的。

**语法**：

```java
public Document addSignatureField(Document inDoc,
 String signatureFieldName,
 Integer pageNo,
 PositionRectangle positionRectangle,
 FieldMDPOptionSpec fieldMDPOptionsSpec,
 PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)
```

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF的文档对象</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>签名字段的名称。 此参数是必需的，不能接受null值。</td>
  </tr>
  <tr>
   <td><code>pageNumber</code></td>
   <td>添加签名字段的页码。 有效值为1到文档中包含的页数。 此参数是必需的，不能接受null值。<br /> </td>
  </tr>
  <tr>
   <td><code>positionRectangle</code></td>
   <td>指定签名字段位置的<code>PositionRectangle object</code>。 此参数是必需的，不能接受null值。 如果指定的矩形至少部分不位于指定页面的裁切框中，则会引发<code>InvalidArgumentException</code>。 此外，指定矩形的高度或宽度不能为0或负数。 左下X或左下Y坐标可以为0或更大，但不是负数，并且与页面的裁切框相关。</td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td><code>FieldMDPOptionSpec</code>对象，它指定签名字段后锁定的PDF文档字段。 这是一个可选参数，可以为null。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>指定字段的各种种子值的<code>SeedValueOptions</code>对象。 这是一个可选参数，可以为null。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。 只有加密的文件才需要此参数。</td>
  </tr>
 </tbody>
</table>

以下是一个Java代码示例，用于向PDF文档添加签名字段。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds a signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddSignatureField.class)
public class AddSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addSignatureField(
       inDoc,
       fieldName,
       pageNum,
       post,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 应用文档时间戳 {#apply-document-timestamp}

您可以按照[PAdES 4](https://en.wikipedia.org/wiki/PAdES)规范以编程方式为文档添加时间戳。 您也可以对事务相关文档使用[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)规范。

**语法**： `applyDocumentTimeStamp(Document doc, VerificationTime verificationTime, ValidationPreferences dssPrefs, ResourceResolver resourceResolver, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>包含PDF.<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>VerificationTime</code></td>
   <td>签名应验证的时间<br /> </td>
  </tr>
  <tr>
   <td><code>ValidationPreferences</code> </td>
   <td>用于控制验证配置的首选项。</td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>Granite信任存储区的资源解析程序。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。 仅当文件已加密时才需要此项。</td>
  </tr>
 </tbody>
</table>

以下代码示例根据[PAdES 4](https://en.wikipedia.org/wiki/PAdES)向文档添加时间戳。

```java
package com.adobe.signatures.test;

import java.io.File;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

 @Component
 @Service(value=Test.class)
 public class Test {

     @Reference
     private DocAssuranceService docAssuranceService;

     @Reference
     private SlingRepository slingRepository;

     @Reference
     private JcrResourceResolverFactory jcrResourceResolverFactory ;

     /**
      *
      * @param inputFile - path to the pdf document stored at disk
      * @param outputFile - path to the pdf document where the output needs to be stored
      * @throws Exception
      */
     public void TimeStamp(String inputFile, String outputFile) throws Exception{

         File inFile = new File(inputFile);
         Document inDoc = new Document(inFile);

         File outFile = new File(outputFile);
         Document outDoc = null;

         Session adminSession = null;
         ResourceResolver resourceResolver = null;
         try {

              /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
              the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
              the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
              here we are using the same resource resolver
              */
              adminSession = slingRepository.loginAdministrative(null);
              resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

              VerificationTime verificationTime = getVerificationTimeForPades();
              ValidationPreferences dssPrefs = getValidationPreferences();

              //retrieve specifications for each of the services, you may pass null if you do not want to use that service
              //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
               outDoc = docAssuranceService.applyDocumentTimeStamp(inDoc, verificationTime, dssPrefs, resourceResolver, null);
         }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

         outDoc.copyToFile(outFile);

     }

  public  VerificationTime getVerificationTimeForPades(){

         return VerificationTime.SECURE_TIME_ELSE_CURRENT_TIME;

     }

 /**
       * sets ValidationPreferences
       */
      private static ValidationPreferences getValidationPreferences(){

         ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
         prefs.setPKIPreferences(getPKIPreferences());

         //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected

         return prefs;

     }

   /**
       * sets PKIPreferences
       */
     private static PKIPreferences getPKIPreferences(){
         PKIPreferences pkiPref = new PKIPreferencesImpl();
         pkiPref.setCRLPreferences(getCRLPreferences());
         pkiPref.setPathPreferences(getPathValidationPreferences());
         pkiPref.setOCSPPreferences(getOCSPPref());
         pkiPref.setTSPPreferences(getTspPref());
         return pkiPref;
     }

   /**
      * sets CRL Preferences
      */
     private static CRLPreferences getCRLPreferences(){

         CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
         crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
         crlPrefs.setGoOnline(true);
         return crlPrefs;
     }

     /**
      *
      * sets PathValidationPreferences
      */
     private static PathValidationPreferences getPathValidationPreferences(){
         PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
         pathPref.setDoValidation(true);
         return pathPref;

     }

   public static TSPPreferences getTspPref(){
   TSPPreferencesImpl tspPrefs=new TSPPreferencesImpl();
   char pass[]=new char[9];

   tspPrefs.setTspServerURL("TSPPrefs_ServerURL");
   tspPrefs.setUsername("TSPPrefs_Username");
   tspPrefs.setPassword(pass);
   tspPrefs.setSize(10240);
   return tspPrefs;
   }

     private static OCSPPreferencesImpl getOCSPPref(){
         OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
         ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
         return ocsp;
     }

}
```

### 获取签名 {#getting-signature}

您可以检索要签署或认证的PDF文档中的所有签名字段的名称。 如果您不确定PDF文档中的签名字段名称或验证名称，则以编程方式检索名称。 签名服务返回签名字段的完全限定名称，如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**语法**： `getSignature(Document doc, String signatureFieldName, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>包含PDF.<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>包含签名的签名字段的名称。 指定签名字段的完全限定名称。 使用基于XFA表单的PDF文档时，可以使用签名字段的部分名称。 例如，可以将<code>form1[0].#subform[1].SignatureField3[3]</code>指定为<code>SignatureField3[3]</code>。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。 仅当文件已加密时才需要此项。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例检索PDF文档中给定签名字段的签名信息。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.client.types.PDFSignature;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetSignature.class)
public class GetSignature {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void GetSignature(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignature pdfSignature = docAssuranceService.getSignature(inDoc,"fieldName",null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 获取签名字段列表  {#getting-signature-field-list-nbsp}

您可以检索要签署或认证的PDF文档中的所有签名字段的名称。 如果您不确定PDF文档中的签名字段名称，则可以通过编程方式检索和验证它们。 签名服务返回签名字段的完全限定名称，如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**语法**： `public List <PDFSignatureField> getSignatureFieldList (Document inDoc, UnlockOptions unlockOptions)`

**输入参数**

| 参数 | 描述 |
|---|---|
| `inDoc` | 包含PDF的文档对象 |
| `unlockOptions` | 包含解锁加密文件所需的参数。 仅当文件已加密时才需要此项。 |

以下Java代码示例检索PDF文档中签名字段的名称。

```java
/*************************************************************************
 *
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------
**************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the names of signature fields in a PDF document.
 */

@Component
@Service(value=GetSignatureFields.class)
public class GetSignatureFields {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getSignatureFields(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve the name of the document's signature fields
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        List fieldNames = docAssuranceService.getSignatureFieldList(inDoc,null);

        //Obtain the name of each signature field by iterating through the
        //List object
        Iterator iter = fieldNames.iterator();
        int i = 0 ;
        String fieldName="";
        while (iter.hasNext()) {
            PDFSignatureField signatureField = (PDFSignatureField)iter.next();
            fieldName = signatureField.getName();
            System.out.println("The name of the signature field is " +fieldName);
            i++;
        }
   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 修改签名字段  {#modifying-signature-fields-nbsp}

您可以修改PDF文档中的签名字段。 修改签名字段涉及处理其签名字段锁定字典值或种子值字典值。

字段锁定字典指定签名字段签名时锁定的字段列表。 锁定的字段可阻止用户编辑该字段。 种子值字典包含应用签名时使用的约束信息。 例如，您可以更改在不使签名失效的情况下控制可能发生的操作的权限。

通过修改现有签名字段，可以编辑PDF文档以反映不断变化的业务要求。 例如，新的业务要求要求在签署文档后锁定所有文档字段。

**语法**： `public Document modifySignatureField(Document inDoc, String signatureFieldName, PDFSignatureFieldProperties pdfSignatureFieldProperties, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>包含PDF的文档对象</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>签名字段的名称。 此参数是必需的，不能接受null值。<br /> </td>
  </tr>
  <tr>
   <td><code>pdfSignatureFieldProperties</code></td>
   <td>指定有关签名字段<code>PDFSeedValueOptionSpec</code>和<code>FieldMDPOptionSpec</code>值的信息的对象。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。 仅当文件已加密时才需要此项。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例通过在签名应用于签名字段时锁定表单中的所有字段来修改签名字段。

```java
/*************************************************************************
 *

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.FieldMDPAction;
import com.adobe.fd.signatures.client.types.FieldMDPOptionSpec;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.PDFSeedValueOptionSpec;
import com.adobe.fd.signatures.client.types.PDFSignatureFieldProperties;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.MissingSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignatureFieldSignedException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can modify signature fields that are in a PDF document by using the Java API and web service API. Modifying a signature field involves
 * manipulating its signature field lock dictionary values or seed value dictionary values.
 * A field lock dictionary specifies a list of fields that are locked when the signature field is signed. A locked field prevents users from making
 * changes to the field. A seed value dictionary contains constraining information that is used at the time the signature is applied.
 * For example, you can change permissions that control the actions that can occur without invalidating a signature.
 * By modifying an existing signature field, you can change the PDF document to reflect changing business requirements. For example,
 * a new business requirement may require locking all document fields after the document is signed.
 * This section explains how to modify a signature field by amending both field lock dictionary and seed value dictionary values.
 * Changes made to the signature field lock dictionary result in all fields in the PDF document being locked when a signature field is signed.
 * Changes made to the seed value dictionary prohibit specific types of changes to the document.
 *
 * The following Java code example modifies a signature field named SignatureField1 by locking all fields in the form when a signature is applied to the signature field and ensuring that no changes are allowed.
 * After the Signature service returns the PDF document that contains the modified signature field
 */

@Component
@Service(value=ModifySignatureField.class)
public class ModifySignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  *
  *
  */
 public void modifySignatureField(String inputFile, String outFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a PDFSignatureFieldProperties
        PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();

         //Create a PDFSeedValueOptionSpec object that stores
         //seed value dictionary information.
         PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();

         //Disallow changes to the PDF document. Any change to the document invalidates
         //the signature
         seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);

         //Create a FieldMDPOptionSpec object that stores
         //signature field lock dictionary information.
         FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();

         //Lock all fields in the PDF document
         fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);

         //Set dictionary information
         fieldProperties.setSeedValue(seedOptionsSpec);
         fieldProperties.setFieldMDP(fieldMDPOptionsSpec);

         //Modify the signature field
         //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
         Document modSignatureField =  docAssuranceService.modifySignatureField(inDoc,fieldName,fieldProperties,null);

        //save the modSignatureField
         modSignatureField.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 认证PDF文档  {#certifying-pdf-documents-nbsp}

您可以通过使用称为认证签名的特定签名类型来认证PDF文档，从而保护文档安全。 认证签名与数字签名在以下方面有所不同：

* 它必须是应用于PDF文档的第一个签名。 换言之，在应用经验证的签名时，文档中的其他签名字段必须未签名。 PDF文档中只允许一个认证签名。 要签署和认证PDF文档，请在签署之前进行认证。 认证PDF文档后，您可以对附加签名字段进行数字签名。
* 文档的作者或创建者可以指定以特定方式修改文档，而不会使已验证签名失效。 例如，文档可以允许填写表单或添加注释。 如果作者指定不允许进行某些修改，Acrobat将限制用户以这种方式修改文档。 如果进行了此类修改，则认证签名无效。 此外，Acrobat会在用户打开文档时发出警告。 （对于未验证的签名，不会阻止修改，并且正常的编辑操作不会使原始签名失效。）
* 在签署时，将扫描文档以查找可能会使文档内容不明确或误导性的特定内容类型。 例如，注释可能会遮蔽页面上的某些文本，而这些文本对于了解正在认证的内容非常重要。 可以就此类内容提供解释（法律证明）。

**语法**：

```java
secureDocument(Document inDoc, EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions, ReaderExtensionOptions readerExtensionOptions, UnlockOptions unlockOptions)
```

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>文档输入PDF文档<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>包含加密PDF文档<br />所需的参数 </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>包含签名/认证PDF文档所需的选项</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>包含Reader扩展PDF文档所需的选项</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。仅当文件已加密时才需要此参数。<br /> </td>
  </tr>
 </tbody>
</table>

以下代码示例验证一个基于PDF文件的PDF文档。

```java
/*************************************************************************

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * You can secure a PDF document by certifying it with a particular type of signature called a certified signature.
 * A certified signature is distinguished from a digital signature in these ways:
 *
 * It must be the first signature applied to the PDF document; that is, at the time the certified signature is applied, any other signature fields in the document must be unsigned.
 * Only one certified signature is permitted in a PDF document. If you want to sign and certify a PDF document, you must certify it before signing it.
 * After you certify a PDF document, you can digitally sign additional signature fields.
 *
 * The author or originator of the document can specify that the document can be modified in certain ways without invalidating the certified signature. For example,
 * the document may permit filling in forms or commenting. If the author specifies that a certain modification is not permitted, Acrobat restricts users from modifying the document
 * in that way. If such modifications are made, such as by using another application, the certified signature is invalid and Acrobat issues a warning when a user opens the document.
 * (With non-certified signatures, modifications are not prevented, and normal editing operations do not invalidate the original signature.)
 *
 * At the time of signing, the document is scanned for specific types of content that could make the contents of a document ambiguous or misleading. For example, an annotation could
 * obscure some text on a page that is important for understanding what is being certified. An explanation (legal attestation) can be provided about such content.
 * You can programmatically certify PDF documents by using the Signature service Java API or the Signature web service API. When certifying a PDF document, you must reference a security
 * credential that exists in the Credential service.
 *
 * Note: When certifying and signing the same PDF document, if the certify signature is not trusted, a yellow triangle appears next to the first sign signature when you open the PDF document in Acrobat or Adobe Reader.
 * The certifying signature must be trusted to avoid this situation.
 *
 * The following Java code example certifies a PDF document that is based on a PDF file.
 *
 * PreRequisites - Digital certificate for certifying the document has to be uploaded on AEM Key Store.
 *
 */

@Component
@Service(value=Certify.class)
public class Certify {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void certify(String inputFile, String outputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //we are not extending the reader in this case, so passing null
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    try {
    outDoc = docAssuranceService.secureDocument(inDoc, null, getCertificationOptions(resourceResolver), null,null);
   } catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }

        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA256;

        //Reason for signing/certifying
        String reason = "Reason";

        //location of the signer
        String location = "Location";

        //contact info of the signer
        String contactInfo = "Contact Info";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, false, true, true, TextDirection.AUTO);
        signatureOptions.setLockCertifyingField(true);
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 保护文档 {#securing-documents}

secureDocument允许您按特定顺序单独或以任何组合方式加密、签名/认证和读取扩展PDF文档。 要访问任何此功能，请传递相应的参数。 如果为null，则假定不需要特定处理。

**使用密码加密PDF文档**

使用密码加密PDF文档时，用户必须指定密码才能在Adobe Reader或Acrobat中打开PDF文档。 此外，在其他AEM Forms Document Services操作使用该文档之前，必须解锁已密码加密的PDF文档。

**使用证书加密PDF文档**

基于证书的加密允许您使用公钥技术为特定收件人加密文档。

可以为各种收件人授予该文档的不同权限。 公钥技术使加密的许多方面成为可能。

算法用于生成两个大数字，称为具有以下属性的键：

* 一个密钥用于加密一组数据。 之后，只能使用另一个密钥来解密数据。
* 一个键和另一个键无法区分。
* 其中一个密钥充当用户的私钥。 仅用户有权访问此键很重要。
* 另一个密钥是用户的公钥，可以与其他用户共享。

公钥证书包含用户的公钥和标识信息。 X.509格式用于存储证书。 证书通常由证书颁发机构(CA)颁发并进行数字签名，CA是一个公认的实体，提供对证书有效性的信任度量。 证书有过期日期，过期后不再有效。

此外，证书吊销列表(CRL)提供在证书过期日期之前被吊销的证书的相关信息。 证书颁发机构定期发布CRL。 证书吊销状态也可以通过网络上的联机证书状态协议(OCSP)进行检索。

>[!NOTE]
>
>在使用证书加密PDF文档之前，必须确保将证书添加到AEM信任存储区。

**将使用权限应用于PDF文档**

您可以使用PDF扩展Java客户端API和Web服务向Reader文档应用使用权限。 使用权限与默认在Acrobat中可用，但在Adobe Reader中不可用的功能相关，例如向表单添加注释或填写表单字段并保存表单的功能。 已应用使用权限的PDF文档称为启用权限的文档。 在Adobe Reader中打开启用了权限的文档的用户可以执行为该特定文档启用的操作。

在Reader使用证书扩展PDF文档之前，必须确保将证书添加到AEM Keystore。

**对PDF文档进行数字签名**

可以将数字签名应用于PDF文档，以提供一定级别的安全性。 数字签名（如手写签名）提供了一种方法，签名者可通过它识别自己并就文档发表声明。

用于对文档进行数字签名的技术，有助于确保签名者和收件人都清楚已签署的内容，并且确信文档在签署后未发生更改。

PDF文档采用公钥技术签名。 签名者有两个密钥：公钥和私钥。 私钥存储在用户的凭据中，该凭据在签名时必须可用。

公钥存储在用户的证书中，收件人必须能够使用该证书来验证签名。 可在证书颁发机构(CA)分发的证书吊销列表(CRL)和联机证书状态协议(OCSP)响应中找到有关吊销证书的信息。 签名时间可以从称为时间戳颁发机构的受信任源获得。

>[!NOTE]
>
>在对PDF文档进行数字签名之前，必须确保在AEM Keystore中添加凭据。 凭据是用于签名的私钥。

>[!NOTE]
>
>AEM FormsPDF还支持对文档进行数字签名的&#x200B;*[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)*&#x200B;规范。

**认证PDF文档**

您可以通过使用称为认证签名的特定签名类型来认证PDF文档，从而保护文档安全。 认证签名与数字签名在以下方面有所不同：

它必须是应用于PDF文档的第一个签名；即在应用已验证签名时，文档中的任何其他签名字段都必须未签名。

PDF文档中只允许一个认证签名。 如果要签署和认证PDF文档，则必须在签署之前对其进行认证。

认证PDF文档后，您可以对附加签名字段进行数字签名。

文档的作者或创建者可以指定以特定方式修改文档，而不会使已验证签名失效。

例如，文档可能允许填写表单或添加注释。 如果作者指定不允许进行某些修改，

Acrobat限制用户以这种方式修改文档。 如果进行了此类修改，例如使用其他应用程序，则认证签名无效，Acrobat会在用户打开文档时发出警告。 （对于未验证的签名，不会阻止修改，并且正常的编辑操作不会使原始签名失效。）

在签署时，将扫描文档以查找可能会使文档内容不明确或误导性的特定内容类型。

例如，注释可能会遮蔽页面上的某些文本，而这些文本对于了解正在认证的内容非常重要。 可以就此类内容提供解释（法律证明）。

>[!NOTE]
>
>在对PDF文档进行数字签名之前，必须确保在AEM Keystore中添加凭据。 凭据是用于签名的私钥。

**语法**：

```java
secureDocument(Document inDoc,
 EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions,
 ReaderExtensionOptions readerExtensionOptions,
 UnlockOptions unlockOptions)
```

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>文档输入PDF文档<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>包含加密PDF文档<br />所需的参数 </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>包括签名/认证PDF文档所需的选项</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>包含Reader扩展PDF文档所需的选项</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>包含解锁加密文件所需的参数。仅当文件已加密时才需要此参数。<br /> </td>
  </tr>
 </tbody>
</table>

**示例1**：此示例用于执行密码加密、验证签名字段和Reader扩展PDF文档。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.PasswordEncryptionCompatability;
import com.adobe.fd.encryption.client.PasswordEncryptionOption;
import com.adobe.fd.encryption.client.PasswordEncryptionOptionSpec;
import com.adobe.fd.encryption.client.PasswordEncryptionPermission;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * password encryption, certifying a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptCertifyExtend.class)
public class PassEncryptCertifyExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void SecureDocument(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getPassEncryptionOptions(), getCertificationOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getPassEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

  //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
        PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();

        //Specify the PDF document resource to encrypt
        passSpec.setEncryptOption(PasswordEncryptionOption.ALL);

        //Specify the permission associated with the password
        //These permissions enable data to be extracted from a password
        //protected PDF form
        List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
        passSpec.setPermissionsRequested(encrypPermissions);

        //Specify the Acrobat version
        passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);

        //Specify the password values
        passSpec.setDocumentOpenPassword("OpenPassword");
        passSpec.setPermissionPassword("PermissionPassword");

        //Set the encryption type to Password Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_PASSWORD);
        encryptionOptions.setPasswordEncryptionOptionSpec(passSpec);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

**示例2**：此示例用于执行PKI加密、签名字段和Reader扩展PDF文档。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.CertificateEncryptionCompatibility;
import com.adobe.fd.encryption.client.CertificateEncryptionIdentity;
import com.adobe.fd.encryption.client.CertificateEncryptionOption;
import com.adobe.fd.encryption.client.CertificateEncryptionOptionSpec;
import com.adobe.fd.encryption.client.CertificateEncryptionPermissions;
import com.adobe.fd.encryption.client.Recipient;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * certificate encryption, signing a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for encrypting the document has to be uploaded on Granite Trust Store
       Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptSignExtend.class)
public class PassEncryptSignExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void CertEncryptSignReaderExtend(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you do not want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getCertEncryptionOptions(), getSignatureOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getCertEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

        //Set the encryption type to Certificate Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_CERTIFCATE);

  //Set the List that stores PKI information
  List<CertificateEncryptionIdentity> pkiIdentities = new ArrayList<CertificateEncryptionIdentity>();

  //Set the Permission List
  List<CertificateEncryptionPermissions> permList = new ArrayList<CertificateEncryptionPermissions>();
  permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;

  //Create a Recipient object to store certificate information
  Recipient recipient = new Recipient();

  //Specify the alias of the public certificate present in the trust store that is used to encrypt the document
  recipient.setX509Cert("alias");
  /*
   * An alternative to add a certificate is by providing the alias
   * of the certificate stored in AEM trust store.
   * recipient.setAlias(alias);
   */

  //Create an EncryptionIdentity object
  CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
  encryptionId.setPerms(permList);
  encryptionId.setRecipient(recipient);

  //Add the EncryptionIdentity to the list
  pkiIdentities.add(encryptionId);

  //Set encryption run-time options
  CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
  certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
  certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_9);

  //Set the certificate encryption option
  encryptionOptions.setCertOptionSpec(certOptionsSpec)

  //Set the PKI Identities in encryption Options
        encryptionOptions.setPkiIdentities(pkiIdentities);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

如果Reader扩展PDF文档时显示以下错误消息：

```javascript
org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.ThreadDeath: null at com.adobe.internal.pdftoolkit.services.javascript.GibsonContextFactory.observeInstructionCount(GibsonContextFactory.java:138)
```

这意味着Reader扩展服务在定义的超时间隔内无法执行文档中使用的JavaScripts。

使用以下方式管理PDF文档中为JavaScripts定义的超时间隔：

```javascript
ReaderExtensionsOptionSpec optionSpec = new ReaderExtensionsOptionSpec(usageRights, message);
optionSpec.setJsScriptExecutionTimeoutInterval(100);
```

其中100是指为执行JavaScripts而定义的超时间隔（以秒为单位）。 为超时间隔设置适当的值。

### 获取凭据使用权限 {#getting-credential-usage-rights}

要获取给定`credentialAlias`指定的凭据的使用权限信息，请从`SecureDocument` API中调用此API。

**语法**： `getCredentialUsageRights(String credentialAlias, ResourceResolver resourceResolver)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>credentialAlias</code><br /> </td>
   <td>指定凭据的<code>credentialAlias</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>credentialPassword</code><br /> </td>
   <td>如果凭据已加密，则凭据的密码为null；如果凭据未加密，则需要使用null。<br /> </td>
  </tr>
 </tbody>
</table>

以下示例获取指定凭据的使用权限信息。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 *
 */
@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
 private ResourceResolverFactory resourceResolverFactory;
public void getCredentialUsageRights() {
  try {

   GetUsageRightsResult usageRightsResult = docAssuranceService.getCredentialUsageRights("production",
     resourceResolverFactory.getAdministrativeResourceResolver(null));

   System.out.println("Credential usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  }
 }
}
```

### 获取文档使用权限 {#getting-document-usage-rights}

要获取给定文档的使用权限信息，请在`docAssuranceService`API中调用此API。

**语法**： `getDocumentUsageRights(Document inDocument, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>要从<br />获取使用权限信息的文档 </td>
  </tr>
 </tbody>
</table>

以下示例代码返回文档的使用权限信息。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void getDocumentUsageRights() {
  Document inputDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/GetUsageRightsInfo/02_fromAcrobat7.0.8_Acro700_UB8_BS_signed_commenting.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   GetUsageRightsResult usageRightsResult = docAssuranceService.getDocumentUsageRights(inputDocument, unlockOptions);

   System.out.println("Document usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  } finally {
//   if (inputDocument != null) {
//    inputDocument.dispose(); //dispose off the document.
//   }
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

### 删除使用权限 {#removing-usage-rights}

您可以通过从`docAssuranceService`API中调用`removeUsageRights`API来删除文档的使用权限。

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>要从中删除使用权限的文档。<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>包含解锁加密文件所需的参数。 仅当文件已加密时才需要此项。<br /> </td>
  </tr>
 </tbody>
</table>

以下示例删除给定文档的使用权限。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void removeDocumentUsageRights() {
  Document inputDocument = null;
  Document outDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/RemoveUsageRights/01_Ubiquitized_50-267_PDF1.5_UB2_Rights.pdf";

   //Name of the output file where result will be saved.
   String outputFileName = "C:/RETest/output/samples/removeUsageRightsOutput.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   //Specify null encryption options and signatures options.
   //If requirement is also to encrypt and sign the document then, corresponding options can also be specified.
   outDocument = docAssuranceService.removeUsageRights(inputDocument, unlockOptions);

   File outputdir = new File("C:/RETest/output/samples");
   outputdir.mkdirs();

   outDocument.copyToFile(new File(outputFileName));
  } catch (Exception e) {
   e.printStackTrace();
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

#### 验证数字签名 {#verifying-digital-signatures}

可以验证数字签名，以确保未修改已签名的PDF文档，并且数字签名有效。 验证数字签名时，您可以检查签名的状态和签名属性，如签名者的身份。 在信任数字签名之前，建议您对其进行验证。 验证数字签名时，引用包含数字签名的PDF文档。

**语法**： `verify( inDoc, signatureFieldName, revocationCheckStyle, verificationTime, dssPrefs, ResourceResolver resourceResolver)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>包含PDF<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code class="code">signatureField
      Name</code><br /> </td>
   <td>要验证的签名字段的名称。 可以提供完全限定名或部分名<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>用于管理验证期间遇到的证书的吊销检查的选项</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>签名应验证的时间</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>用于控制各种验证配置的首选项。 对于加密文档，使用设置解锁选项 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Granite信任存储区的资源解析程序</td>
  </tr>
 </tbody>
</table>

此示例代码使用`DocAssuranceService`验证加密的PDF文档中的签名字段。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.IdentityInformation;
import com.adobe.fd.signatures.client.types.IdentityStatus;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of a signature field in an already Encrypted PDF Document
 *
 * Digital signatures can be verified to ensure that a signed PDF document was not modified and that the digital signature is valid.
 * When verifying a digital signature, you can check the signature's status and the signature's properties, such as the signer's identity.
 * Before trusting a digital signature, it is recommended that you verify it. When verifying a digital signature, reference a PDF document
 * that contains a digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyFieldEncryptedPDF.class)
public class VerifyFieldEncryptedPDF {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyFieldEncryptedPDF(String inputFile,String fieldName) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

         //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

           //Specify the name of the signature field

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.AlwaysCheck;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFSignatureVerificationInfo  signInfo = docAssuranceService.verify(
                 inDoc,
                 fieldName,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get the Signature Status
             SignatureStatus sigStatus = signInfo.getStatus();
             String myStatus="";

             //Determine the status of the signature
             if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                 myStatus = "The signatures in the dynamic PDF form are unknown";
             else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                 myStatus = "The signatures in the PDF document are unknown";
             else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a certified PDF form are valid";
             else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a signed dynamic PDF form are valid";
             else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                 myStatus = "The signatures in a certified PDF document are valid";
             else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                 myStatus = "The signatures in a signed PDF document are valid";
             else if (sigStatus == SignatureStatus.SignatureFormatError)
                 myStatus = "The format of a signature in a signed document is invalid";
             else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                 myStatus = "No changes were made to the signed dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                 myStatus = "No changes were made to the signed PDF document";
             else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified PDF document";
             else if (sigStatus == SignatureStatus.DocSigWithChanges)
                 myStatus = "There were changes to a signed PDF document";
            else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                 myStatus = "There were changes made to the PDF document.";

             //Get the signature type
             SignatureType sigType = signInfo.getSignatureType();
             String myType = "";

             if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                    myType="Certification";
             else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                    myType="Recipient";

             //Get the identity of the signer
             IdentityInformation signerId = signInfo.getSigner();
             String signerMsg = "";

            if (signerId.getStatus() == IdentityStatus.UNKNOWN)
                signerMsg = "Identity Unknown";
            else if (signerId.getStatus() == IdentityStatus.TRUSTED)
                signerMsg = "Identity Trusted";
            else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
                signerMsg = "Identity Not Trusted";

            //Get the Signature properties returned by the Signature service
            SignatureProperties sigProps = signInfo.getSignatureProps();
            String signerName =  sigProps.getSignerName();

           System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        pkiPref.setOCSPPreferences(getOCSPPref());
        pkiPref.setTSPPreferences(getTspPref());
        return pkiPref;
    }

    private static TSPPreferences getTspPref(){
     TSPPreferencesImpl tsp = new TSPPreferencesImpl();
     tsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return tsp;
    }
    private static OCSPPreferencesImpl getOCSPPref(){
     OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
     ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return ocsp;
    }
    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(true);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 验证多个数字签名 {#verifying-multiple-digital-signatures}

通过AEM，您可以在PDF文档中验证数字签名。 如果PDF文档所遵循的业务流程需要由多个签名者进行签名，则该文档可以包含多个数字签名。 例如，金融交易需要贷款官员和经理的签名。 您可以使用签名服务API验证PDF文档中的所有签名。 验证多个数字签名时，您可以检查每个签名的状态和属性。 在信任数字签名之前，Adobe建议您对其进行验证。

**语法**： `verifyDocument(Document doc, RevocationCheckStyle revocationCheckStyle, VerificationTime verificationTime, ValidationPreferences prefStore, ResourceResolver resourceResolver)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>包含PDF<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>用于管理验证期间遇到的证书的吊销检查的选项</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>签名应验证的时间</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>用于控制各种验证配置的首选项。 对于加密文档，使用设置解锁选项 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Granite信任存储区的资源解析程序</td>
  </tr>
 </tbody>
</table>

以下示例代码使用DocAssuranceService验证已加密的PDF文档中的签名字段。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.List;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFDocumentVerificationInfo;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of all the signature fields in an already Encrypted PDF Document
 *
 * Assume that a PDF document contains multiple digital signatures as a result of a business process that requires signatures from multiple
 * signers. For example, consider a financial transaction that requires both a loan officer's and a manager's signature. You can use the
 * Signature service Java API or web service API to verify all signatures within the PDF document. When verifying multiple digital signatures,
 * you can check the status and properties of each signature. Before you trust a digital signature, it is recommended that you verify it. It
 * is recommended that you are familiar with verifying a single digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyEncryptedPDFDoc.class)
public class VerifyEncryptedPDFDoc {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyEncryptedPDFDoc(String inputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.CheckIfAvailable;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFDocumentVerificationInfo  docInfo = docAssuranceService.verifyDocument(
                 inDoc,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get a list of all signatures that are in the PDF document
             List allSignatures = docInfo.getVerificationInfos();

           //Create an Iterator object and iterate through
           //the List object
           Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();

           while (iter.hasNext()) {
                  PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();

                  //Get the Signature Status
                     SignatureStatus sigStatus = signInfo.getStatus();
                     String myStatus="";

                   //Determine the status of the signature
                     if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                         myStatus = "The signatures in the dynamic PDF form are unknown";
                     else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                         myStatus = "The signatures in the PDF document are unknown";
                     else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a certified PDF form are valid";
                     else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a signed dynamic PDF form are valid";
                     else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                         myStatus = "The signatures in a certified PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                         myStatus = "The signatures in a signed PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignatureFormatError)
                         myStatus = "The format of a signature in a signed document is invalid";
                     else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                         myStatus = "No changes were made to the signed dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                         myStatus = "No changes were made to the signed PDF document";
                     else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified PDF document";
                     else if (sigStatus == SignatureStatus.DocSigWithChanges)
                         myStatus = "There were changes to a signed PDF document";
                    else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                         myStatus = "There were changes made to the PDF document.";

                     //Get the signature type
                    SignatureType sigType = signInfo.getSignatureType();
                    String myType = "";

                    if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                        myType="Certification";
                    else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                        myType="Recipient";

                    //Get the Signature properties returned by the Signature service
                    SignatureProperties sigProps = signInfo.getSignatureProps();
                    String signerName =  sigProps.getSignerName();

                   System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
               }
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the document is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 删除数字签名 {#removing-digital-signatures}

只有在删除以前的数字签名之后，才能将新的数字签名应用到签名字段。 无法覆盖数字签名。 如果尝试将数字签名应用于已包含签名的签名字段，则会发生异常。

**语法**： `clearSignatureField(Document inDoc, String signatureFieldName, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>包含PDF<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>签名字段<br />的名称 </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>包含解锁加密文件所需的参数。仅当文件已加密时才需要此参数<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例从签名字段中删除数字签名。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file
*from a source other than Adobe, then your use, modification, or distribution of it requires
*the prior written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures must be removed from a signature field before a newer digital signature can be applied.
 * A digital signature cannot be overwritten.
 * If you attempt to apply a digital signature to a signature field that contains a signature, an exception occurs
 *
 *The following Java code example removes a digital signature from a signature field named SignatureField1.
 *The name of the PDF file that contain the signature field is LoanSigned.pdf
 */

@Component
@Service(value=ClearSignatureField.class)
public class ClearSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;
 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  * @throws Exception
  */
 public void clearSignatureField(String inputFile, String outFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Clear the signature field
        //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        Document outPDF = docAssuranceService.clearSignatureField(inDoc,fieldName,null);

        //save the outPDF
        outPDF.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 获取认证签名字段 {#getting-certifying-signature-field}

您可以检索要签署或认证的PDF文档中的所有签名字段的名称。 如果您不确定PDF文档中的签名字段名称，或者希望验证这些名称，则可以通过编程方式检索它们。 签名服务返回签名字段的完全限定名称，如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**语法**： `getCertifyingSignatureField(Document inDoc, UnlockOptions unlockOptions)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>包含PDF.<br />的文档对象 </td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>UnlockOptions包括解锁加密文件所需的参数。 仅当文件已加密时才需要此项。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例检索用于证明文档的签名字段。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the ignature field that was used to certify the document.
 */

@Component
@Service(value=GetCertifyingSignatureField.class)
public class GetCertifyingSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getCertifyingSignatureField(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignatureField pdfSignature = docAssuranceService.getCertifyingSignatureField(inDoc,null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 获取PDF加密类型 {#getting-pdf-encryption-type}

您可以检索要签署或认证的PDF文档中的所有签名字段的名称。 如果您不确定PDF文档中的签名字段名称，或者希望验证这些名称，则可以通过编程方式检索它们。 签名服务返回签名字段的完全限定名称，如`asform1[0].grantApplication[0].page1[0].SignatureField1[0]`。

**语法**： `void getPDFEncryption(Document inDoc)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>作为输入提供的文档。 它可能已加密，也可能未加密。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例检索PDF文档中给定签名字段的签名信息。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.encryption.client.EncryptionTypeResult;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetPDFEncryption.class)
public class GetPDFEncryption {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getPDFEncryption(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        EncryptionTypeResult encryptionTypeResult = docAssuranceService.getPDFEncryption(inDoc);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 从PDF中删除密码加密 {#removing-password-encryption-from-pdf}

从PDF文档中删除基于密码的加密，以便用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。 从PDF文档中删除基于密码的加密后，该文档不再安全。

**语法**： `Document removePDFPasswordSecurity (Document inDoc,String password)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>作为输入提供的文档。 它必须受密码保护。<br /> </td>
  </tr>
  <tr>
   <td><code>password</code><br /> </td>
   <td>文档打开或权限密码，用于从该文档中删除安全性。<br /> </td>
  </tr>
 </tbody>
</table>

以下代码示例从PDF文档中删除基于密码的加密。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;
    import java.io.FileNotFoundException;
    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.jcr.api.SlingRepository;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes password-based encryption from a PDF document.
    * The master password value used to remove password-based encryption is PermissionPassword
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePasswordEncryption.class)
    public class RemovePasswordEncryption {

    // Create reference for DocAssuranceService
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    /**
    * The below sample code demonstrates removing password encryption from a PDF using AEM EncryptionService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_out.pdf"
    * @throws Exception
    */
    public void removePasswordEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

        try{

        String password = "PermissionPassword"; //master password with which the pdf was encrypted
                    //in case if the pdf is encrypted only with user password, specify the
                    //user password
        //Remove password-based encryption from the PDF document
        outDoc = docAssuranceService.removePDFPasswordSecurity(inDoc,password);

        }finally{
                    /**
                    * always close the PDFDocument object after your processing is done.
                    */
                    if(inDoc != null){
                        inDoc.close();
                    }

            }

            outDoc.copyToFile(outFile);

    }

    }
```

### 正在删除证书加密 {#removing-certificate-encryption}

您可以从PDF文档中删除基于证书的加密，以便用户在Adobe Reader或Acrobat中打开PDF文档。 要从使用证书加密的PDF文档中删除加密，请引用私钥。 从PDF文档中删除加密后，该加密不再安全。

**语法**： `removePDFCertificateSecurity(Document inDoc, String alias, ResourceResolver resourceResolver)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>表示证书加密的PDF文档的Document对象。<br /> </td>
  </tr>
  <tr>
   <td><code>alias</code><br /> </td>
   <td>与Granite Trust Store中用于从PDF文档中删除基于证书的加密的密钥对应的别名。<br /> </td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>ResourceResolver ，用于访问特定用户的密钥存储以提取凭据。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例从PDF文档中删除基于证书的加密。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;

    import javax.jcr.Session;

    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.api.resource.ResourceResolver;
    import org.apache.sling.jcr.api.SlingRepository;
    import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes certificate-based encryption from a PDF document
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePKIEncryption.class)
    public class RemovePKIEncryption {

    // Create reference for docAssuranceServiceInterface
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    @Reference
        private JcrResourceResolverFactory jcrResourceResolverFactory ;

    /**
    * The below sample code demonstrates encrypting PDF with Password using AEM docAssuranceService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_Encrypted.pdf"
    *
    * @throws Exception
    */
    public void removePKIEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

            Session adminSession = null;
            ResourceResolver resourceResolver = null;
            try{
        adminSession = slingRepository.loginAdministrative(null);
        resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

        //Remove certificate-based encryption from the PDF document
        /**
        * Here the alias("encryption") of the private credential stored in the keystore of the
        * user has been provided with the user's resource resolver
        */
        outDoc = docAssuranceService.removePDFCertificateSecurity(inDoc, "encryption",resourceResolver);

            }catch(Exception e){

            // TODO Auto-generated catch block
            }finally{
                /**
                * always close the PDFDocument object after your processing is done.
                */
                if(inDoc != null){
                    inDoc.close();
                }
                if(adminSession != null && adminSession.isLive()){
                    if(resourceResolver != null){
                        resourceResolver.close();
                    }
                    adminSession.logout();
                }
            }

            outDoc.copyToFile(outFile);
    }

    }
```

## 输出服务 {#output-service}

Output服务提供用于渲染.pdf、.pcl、.zpl和.ps格式的XDP文件的API。 该服务支持以下API：

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p)：**&#x200B;通过将表单设计与存储在网络位置、本地文件系统或HTTP位置上的数据合并为文本值来生成PDF文档。

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p)：**&#x200B;通过将表单设计与应用程序中存储的数据合并来生成PDF文档。
* **[generatePDFOutputBatch](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutputbatch-p)：**&#x200B;将表单设计与数据合并以创建PDF文档。 （可选）为每个记录生成元数据文件，或将输出保存到PDF文件。
* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p)：**&#x200B;从表单设计和存储在网络位置、本地文件系统或HTTP位置的数据文件生成PCL、PostScript或ZPL输出作为文本值。

* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p)：**&#x200B;从表单设计和存储在应用程序中的数据文件中生成PCL、PostScript和ZPL输出。

### generatePDFOutput {#generatepdfoutput}

generatePDFOutput API通过将表单设计和数据合并来生成PDF文档。 （可选）为每个记录生成元数据文件，或将输出保存到PDF文件。 将表单设计或存储在网络位置、本地文件系统或HTTP位置上的数据作为文字值使用generatePDFOutput API。 如果表单设计和XML数据存储在应用程序中，请使用[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API。

**语法：** `Document generatePDFOutput(String uriOrFileName, Document data, PDFOutputOptions options);`

#### 输入参数 {#input-parameters}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>uriOrFileName</td>
   <td>指定输入文件的路径和名称。 文件的类型可以是PDF或XDP。 如果仅指定文件名，则相对于在options中指定的contentRoot读取文件。</td>
  </tr>
  <tr>
   <td>数据</td>
   <td>包含与PDF文档合并的数据的XML文件。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF变量的值。 选项参数接受类型为PDFOutputOptions的对象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例通过将表单设计与XML文件中存储的数据合并来生成PDF文档。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput(String contentRoot,File inputXML,String templateStr,String acrobatVersion,String tagged,String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

    try {

            PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);         if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

            {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {             option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

            }

            if (tagged.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if (linearized.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if(locale!=null)

            {

                option.setLocale(locale);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePDFOutput(templateStr,new Document(in),option);         File toSave = new File(outputFolder+"Output.pdf");

            doc.copyToFile(toSave);

            return toSave;

        } catch (OutputServiceException e) {

            e.printStackTrace();

        }catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }finally{

                    doc.dispose();

        }

        return null;

    }
```

### generatePDFOutput {#generatepdfoutput-1}

generatePDFOutput API通过将表单设计和数据合并来生成PDF文档。 （可选）为每个记录生成元数据文件，或将输出保存到PDF文件。 将generatePrintedOutput API用于表单设计或存储在应用程序中的数据。 如果表单设计和XML数据存储在网络位置、本地或HTTP位置作为文本值，请使用[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API。

**语法：** `Document generatePDFOutput(Document inputdocument, Document data, PDFOutputOptions options)`

#### 输入参数 {#input-parameter}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>指定输入文件的路径和名称。 文件的类型可以是PDF或XDP。 如果仅指定文件名，则相对于在options中指定的contentRoot读取文件。<br /> </td>
  </tr>
  <tr>
   <td>数据</td>
   <td>包含与PDF文档合并的数据的XML文件。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF变量的值。 options参数接受PDFOutputOptions类型的对象。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例通过将表单设计与XML文件中存储的数据合并来生成PDF文档。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput2(String contentRoot, File inputXML, File templateStr, String acrobatVersion, String tagged, String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

        try {

                PDFOutputOptions option = new PDFOutputOptions();             option.setContentRoot(contentRoot);
                if(locale!=null)

                {

                    option.setLocale(locale);

                }

                if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

                {

                    option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

                }

                if (tagged.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                if (linearized.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                InputStream inputXMLStream = new FileInputStream(inputXML);

                InputStream templateStream = new FileInputStream(templateStr);;

                doc = outputService.generatePDFOutput(new Document(templateStream),new             Document(inputXMLStream),option);

                        File toSave = new File(outputFolder,"Output.pdf");

                        doc.copyToFile(toSave);

                        return toSave;

                    } catch (OutputServiceException e) {

                            e.printStackTrace();

                }catch (FileNotFoundException e) {

                            e.printStackTrace();

                } catch (IOException e) {

                            e.printStackTrace();

                }finally{

                                doc.dispose();

                }

                    return null;

    }
```

### generatePDFOutputBatch {#generatepdfoutputbatch}

将表单设计和数据合并以创建PDF文档。 （可选）为每个记录生成元数据文件，或将输出保存到PDF文件。 将generatePDFOutputBatch API用于表单设计或存储在网络位置、本地文件系统或HTTP位置上的数据作为文字值。

**语法：** `BatchResult generatePDFOutputBatch(Map templates, Map data, PDFOutputOptions options, BatchOptions batchOptions);`

#### 输入参数 {#input-parameters-1}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>指定键和模板文件名的映射。<br /> </td>
  </tr>
  <tr>
   <td>数据</td>
   <td>指定键和数据文档的映射。 如果键不为null，则使用模板映射中指定的相应键的模板呈现数据文档。 </td>
  </tr>
  <tr>
   <td>options</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF变量的值。 options参数接受PDFOutputOptions类型的对象。</td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>指定变量<code>generateManyFiles</code>的值。 设置generateManyFiles标志以生成多个文件。 options参数接受BatchOptions类型的对象。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例通过将表单设计与XML文件中存储的数据合并来生成PDF文档。

```java
private ArrayList generatePDFBatch(String contentRoot,String multipleFiles) {

String outputFolder="C:/Output";

    try {

        PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);

        Map templates = new LinkedHashMap();

        Map data = new LinkedHashMap();

        String template1 = "PurchaseOrder.xdp"; String template2 = "CardApp.xdp";         templates.put(template1.substring(0, template1.indexOf(".xdp")),template1);         templates.put(template1.substring(0, template2.indexOf(".xdp")),template2);

        File inputXML1 = new File("c:/InputFolder/PurchaseOrder.xml");

        File inputXML2 = new File("c:/InputFolder/CardApp.xml");

        InputStream in1 = new FileInputStream(inputXML1);

        InputStream in2 = new FileInputStream(inputXML2);

        data.put(template1.substring(0, template1.indexOf(".xdp")),new         Document((in1))); data.put(template1.substring(0,         template1.indexOf(".xdp")),new Document((in2))); BatchOptions bo = new         BatchOptions(); BatchResult ret=null;         if(multipleFiles.equalsIgnoreCase("true"))

        {

            bo.setGenerateManyFiles(true);

            ret = outputService.generatePDFOutputBatch(templates, data, option, bo);

        } else {

            ret = outputService.generatePDFOutputBatch(templates, data, option, new             BatchOptions());

        }

        ArrayList outputs = new ArrayList();

        int counter=0;

        if(ret.getMetaDataDoc() !=null ){

        File toSave = new File(outputFolder+"Output.xml");

        ret.getMetaDataDoc().copyToFile(toSave);

        outputs.add(toSave);

        List<Document> list = ret.getGeneratedDocs();

        for(Document doc:list){

        File toSave = new File(outputFolder,"Output"+"_"+counter+".pdf");         doc.copyToFile(toSave);                    outputs.add(toSave);

        counter++;

        doc.dispose();

        }

        return outputs;

       } catch (OutputServiceException e) {

            e.printStackTrace();

       }catch (FileNotFoundException e) {

            e.printStackTrace();

       }catch (IOException e) {

            e.printStackTrace();

       }

       return null;

}
```

### generatePrintedOutput {#generateprintedoutput}

从表单设计和数据文件生成PCL、PostScript和ZPL输出。 数据文件将与窗体设计合并并设置格式以供打印。 您可以将输出直接发送到打印机或另存为文件。 将generatePrintedOutput API用于表单设计或存储在应用程序中的数据。

**语法：** `Document generatePrintedOutput(String uriOrFileName, Document data, PrintedOutputOptions);`

#### 输入参数 {#input-parameters-2}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>uriOrFileName<br /> </td>
   <td>指定输入文件的路径和名称。 如果仅指定文件名，则相对于在options中指定的contentRoot读取文件。 文件的类型可以是PDF或XDP。<br /> </td>
  </tr>
  <tr>
   <td>数据</td>
   <td>包含与PDF文档合并的数据的XML文件。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>指定contentRoot、locale、AcrobatVersion、linearizedPDF和taggedPDF变量的值。 options参数接受PrintedOutputOptions类型的对象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例从表单设计和数据生成PCL、PostScript和ZPL输出。 输出类型取决于传递给`printConfig`参数的值。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput(String contentRoot,File inputXML,String templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

    try {

            PrintedOutputOptions options = new PrintedOutputOptions();                           options.setContentRoot(contentRoot);

            if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {

                            options.setPrintConfig(PrintConfig.HP_PCL_5e);

                     }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePrintedOutput(templateStr,new             Document(in),options);

            in.close();

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return  toSave;

        } catch (OutputServiceException e) {

             e.printStackTrace();

        }catch (FileNotFoundException e) {

             e.printStackTrace();

        }catch (IOException e) {

             e.printStackTrace();

        }finally{

             doc.dispose();

        }

        return null;

}
```

### generatePrintedOutput {#generateprintedoutput-1}

给定表单设计和数据文件，生成PCL、PostScript和ZPL输出。 数据文件将与窗体设计合并并设置格式以供打印。 输出可以直接发送到打印机或另存为文件。 对表单设计或应用程序中存储的数据使用generatePrintedOutput API。

**语法：** `Document generatePrintedOutput(Document inputdocument, Document data, PrintedOutputOptions);`

#### 输入参数 {#input-parameters-3}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>指定输入文件的路径和名称。 如果仅指定文件名，则相对于在options中指定的contentRoot读取文件。 文件的类型可以是XDP。 </td>
  </tr>
  <tr>
   <td>数据</td>
   <td>包含与PDF文档合并的数据的XML文件。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>此对象用于设置contentRoot、locale、printConfig、copies和paginationOverride的值。 options参数接受PrintedOutputOptions类型的对象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例从表单设计和数据生成PCL、PostScript和ZPL输出。 输出类型取决于传递给`printConfig`参数的值。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput2(File  inputXML,File templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

       try {

            PrintedOutputOptions options = new PrintedOutputOptions();             if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {                                   options.setPrintConfig(PrintConfig.HP_PCL_5e);

            }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

                             }

            InputStream inputXMlStream = new FileInputStream(inputXML);

            InputStream templateStream = new FileInputStream(templateStr); doc =             outputService.generatePrintedOutput(new Document(templateStream),new             Document(inputXMlStream),options);

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return toSave;

            } catch (OutputServiceException e) {

                e.printStackTrace();

            }catch (FileNotFoundException e) {

                e.printStackTrace();

            } catch (IOException e) {

                e.printStackTrace();

            }finally{

                doc.dispose();

            }

            return null;

}
```

### generatePrintedOutputBatch {#generateprintedoutputbatch}

通过将表单设计与数据合并，生成PS、PCL和ZPL格式的文档。 （可选）为每个记录生成元数据文件，或将输出保存到PDF文件。 将generatePrintedOutputBatch API用于表单设计或存储在网络位置、本地文件系统或HTTP位置上的数据作为文字值。

**语法`:`** `BatchResult generatePrintedOutputBatch(Map templates, Map data, PrintedOutputOptions options, BatchOptions batchOptions);`

#### 输入参数 {#input-parameters-4}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>模板<br /> </td>
   <td>指定键和模板文件名的映射。<br /> </td>
  </tr>
  <tr>
   <td>数据</td>
   <td>指定键和数据文档的映射。 如果键不为null，则使用模板映射中相应键的模板呈现数据文档。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>指定PrintedOutputOptions类型的对象。 此对象用于设置contentRoot、locale、printConfig、copies、paginationOverride的值。<br /> </td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>指定变量generateManyFiles的值。 设置generateManyFiles标志以生成多个文件。 options参数接受BatchOptions类型的对象。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例从多个表单设计模板和数据文件批量生成PCL、PostScript和ZPL输出。 输出类型取决于传递给`printConfig`参数的值。

```java
@Reference private OutputService outputService;

private ArrayList generatePrintedOutputBatch(String contentRoot,String multipleFiles,String printConfig) {

String outputFolder="C:/Output";

        try {

                PrintedOutputOptions option = new PrintedOutputOptions();                 option.setContentRoot(contentRoot);

                Map templates = new LinkedHashMap();

                Map data = new LinkedHashMap();

                String template1 = "PurchaseOrder.xdp";

                String template2 = "CardApp.xdp";

                templates.put(template1.substring(0,                 template1.indexOf(".xdp")),template1);                 templates.put(template1.substring(0,                 template2.indexOf(".xdp")),template2);

                File inputXML1 = new                                   File("c:/InputFolder/PurchaseOrder.xml");

                File inputXML2 = new File("c:/InputFolder/CardApp.xml");

                InputStream in1 = new FileInputStream(inputXML1);

                InputStream in2 = new FileInputStream(inputXML2);                  data.put(template1.substring(0,                     template1.indexOf(".xdp")),new Document((in1)));

                 data.put(template2.substring(0,                     template2.indexOf(".xdp")),new Document((in2)));

                 if(printConfig.equalsIgnoreCase("ps"))

                 {

                    option.setPrintConfig(PrintConfig.PS_PLAIN);

                 } else if(printConfig.equalsIgnoreCase("pcl"))

                 {

                    option.setPrintConfig(PrintConfig.HP_PCL_5e);

                 } else if(printConfig.equalsIgnoreCase("zpl")){

                                         option.setPrintConfig(PrintConfig.ZPL300);

                 }

                 option.setContentRoot(contentRoot);

                 BatchOptions bo = new BatchOptions();

                 BatchResult ret =                             outputService.generatePrintedOutputBatch(temp                                    lates, data, option, new                                                     BatchOptions());

                 ArrayList outputs = new ArrayList();

                 int counter=0;

                 if(ret.getMetaDataDoc() !=null ){

                 File toSave = new File(outputFolder,"Output"+".xml");                    ret.getMetaDataDoc().copyToFile(toSave);

                 outputs.add(toSave);

                 List<Document> list = ret.getGeneratedDocs();

                 for(Document doc:list){

                 File toSave = new                                                               File(outputFolder,"Output"+"_"+counter+".                                        "+printConfig);                                    doc.copyToFile(toSave);

                 outputs.add(toSave);

                 counter++;

                 doc.dispose();

                 }

                 return outputs;

          }

            catch (OutputServiceException e) {

                e.printStackTrace();

          }catch (FileNotFoundException e) {

                e.printStackTrace();

          } catch (IOException e) {

                e.printStackTrace();

          }

            return null;

  }
```

## 表单服务 {#forms-service}

Forms服务提供多个API，可将数据导入交互式PDF表单或从其中导出数据。 交互式PDF表单是一种PDF文档，其中包含一个或多个用于显示和收集用户信息的字段。 该服务支持以下API：

* **[exportData](/help/forms/using/aem-document-services-programmatically.md#p-exportdata-p)：**&#x200B;从PDF表单中导出数据。
* **[importData](/help/forms/using/aem-document-services-programmatically.md#p-importdata-p)：**&#x200B;将数据导入交互式PDF表单。

### exportData {#exportdata}

以XML和XDP格式从交互式PDF表单中导出表单数据。

**语法：** `Document exportData(Document xdpOrPdf, DataFormat dataFormat)`

#### 输入参数 {#input-parameters-5}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>xdpOrPdf<br /> </td>
   <td>指定包含XDP或PDF文件的文档对象。 </td>
  </tr>
  <tr>
   <td>数据格式<br /> </td>
   <td>指定导出数据的格式。 它接受enum(XDP， XmlData， Auto)类型的变量。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例以XML和XDP格式从交互式PDF表单中导出表单数据。

#### 样本 {#sample}

```java
@Reference private FormsService formsService;
private File exportData(String  dataFormat, File  inDoc) {

String outputFolder="C:/Output";

InputStream in; Document doc=null;

try {

        in = new FileInputStream(inDoc);

        if(dataFormat.equalsIgnoreCase("xml"))

        {

          doc=formsService.exportData(new Document(in),                                       DataFormat.XmlData);

        }

        else if(dataFormat.equalsIgnoreCase("xdp")) {

        doc =formsService.exportData(new Document(in),                       DataFormat.XDP);

        }

        File toSave = new File(outputFolder,"Output"+"."+dataFormat);

        doc.copyToFile(toSave);

        return toSave;

    } catch (FormsServiceException e) {

       e.printStackTrace();

    }catch (FileNotFoundException e) {

       e.printStackTrace();

    } catch (IOException e) {

       e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

 }
```

### importData {#importdata}

将表单数据导入交互式PDF表单。

**语法：** `Document importData(Document PDF, Document data)`

#### 输入参数 {#input-parameters-6}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>PDF<br /> </td>
   <td>指定包含PDF文件的文档对象。 </td>
  </tr>
  <tr>
   <td>数据<br /> </td>
   <td>包含XML格式数据的XML文件。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例将表单数据导入交互式PDF表单中。

#### 样本 {#sample-1}

```java
@Reference private FormsService formsService

private File importData(File inDoc, File inXML)

{

 String outputFolder="C:/Output";

 Document doc=null;

 try {

        InputStream in = new FileInputStream(inDoc);

        InputStream in2 = new FileInputStream(inXML);

        doc=formsService.importData(new Document(in), new Document(in2));

        File toSave = new File(outputFolder,"Output.pdf");

        doc.copyToFile(toSave);

    } catch (FormsServiceException e) {

         e.printStackTrace();

    }catch (FileNotFoundException e) {

         e.printStackTrace();

    } catch (IOException e) {

         e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

}
```

## PDF Generator服务 {#pdfgeneratorservice}

PDF Generator服务提供一些API，用于将本机文件格式转换为PDF。 它还会将PDF转换为其他文件格式并优化PDF文档的大小。

### GeneratePDF服务 {#generatepdfservice}

GeneratePDFService提供API以将各种文件格式(如.doc、.docx、.ppt、.pptx、.xls、.xlsx、.odp、.odt、.ods、.swf（已弃用）、.jpg、.bmp、.tif、.png、.html和许多其他文件格式)转换为PDF。 它还提供了API以将PDF导出为各种文件格式并优化PDF。 该服务支持以下API：

* **createPDF**：将支持的文件类型转换为PDF文档。 它支持文件格式，如Microsoft Word、Microsoft PowerPoint、Microsoft Excel和Microsoft Project。 除了这些应用程序外，任何第三方通用PDF生成应用程序类型也可以插入到API中。
* **exportPDF**：将PDF文档转换为支持的文件类型。 方法接受PDF作为输入，并以指定的文件类型格式导出PDF的内容。 您可以导出Encapsulated PostScript( eps)、HTML 3.2( htm， html)、带有CSS 1.0( htm， html)、JPEG( jpg， jpeg， jpe)、JPEG2000( jpf， jpx， jp2， j2k， j2c， jpc)、Microsoft Word Document( doc， docx) Microsoft Excel工作簿( xlsx)、Microsoft PowerPoint演示文稿( pptx)、PNG( png)、PDF( ps)、富文本格式( rtf)文本（可访问）(txt)、文本（纯）(txt) HTML( tif， tiff)、XML 1.0( xml)、PostScript/A-1a(sRGB)、TIFF/A-1b、PDF/A-2a(sRGB)、PDF/A-2b(sRGB)、PDF/A-3a(sRGB)、PDF PDF PDF/A-3b(sRGB)格式。 您还可以为PDF输出指定[自定义印前检查配置文件](https://helpx.adobe.com/cn/acrobat/using/preflight-profiles-acrobat-pro.html)。

* **optimizePDF**：优化PDF文档，并将PDF文档从一种类型转换为另一种类型。 方法接受PDF文档作为输入。
* **htmlToPdf2**：将HTML页面转换为PDF文档。 它接受HTML页面的URL作为输入。

>[!NOTE]
>
>对于在AIX操作系统上运行的AEM Forms服务器，HTMLtoPDF API已被弃用。

#### PDF Generator API在Microsoft Windows和Linux上可用 {#pdf-generator-api-available-on-microsoft-windows-and-linux}

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><p><strong>Microsoft Windows </strong></p> </td>
   <td><strong>Linux </strong></td>
  </tr>
  <tr>
   <td>createPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
  <tr>
   <td>htmlToPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
   <td>optimizePDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>exportPDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>OCR PDF (可搜索的PDF)</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
 </tbody>
</table>

#### createPDF {#createpdf}

createPDF API将支持的文件类型转换为PDF文档。 它支持各种文件格式，如Microsoft Word、Microsoft PowerPoint、Microsoft Excel和Microsoft Project。 除了这些应用程序外，任何第三方通用PDF生成应用程序类型也可以插入到API中。

对于转换，只有少数参数是必需的。 输入文档是必需参数。 您可以稍后将安全权限、PDF输出设置和元数据信息应用到输出PDF文档。

createPDF服务会返回一个包含结果的java.util.Map。 映射的键为：

* ConvertedDoc：它包含新创建的PDF文档。
* LogDoc：它包含日志文件。

createPDF服务引发以下异常：

* ConversionException
* InvalidParameterException
* FileFormatNotSupportException

**语法：** `Map createPDF(Document inputDoc, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws InvalidParameterException, ConversionException, FileFormatNotSupportedException;`

#### 输入参数 {#input-parameters-7}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>指定文档对象。 文档对象包含输入文件。 在输入文档上创建com.adobe.aemfd.docmanager.Document对象。 它是必需参数。</td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>输入文件的名称以及扩展名。 它是必需的参数。<br /> </td>
  </tr>
  <tr>
   <td>fileTypeSettings</td>
   <td>它是一个可选参数。</td>
  </tr>
  <tr>
   <td>pdf设置</td>
   <td><p>已转换文档的PDF输出。 您只能应用以下设置：</p>
    <ul>
     <li>高品质_打印<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Minimum_File_Size</li>
    </ul> <p>它是一个可选参数。<br /> </p> </td>
  </tr>
  <tr>
   <td>安全设置</td>
   <td><p>已转换文档的安全设置。 您可以应用以下设置：</p>
    <ul>
     <li>无安全性</li>
     <li>密码安全性<br /> </li>
     <li>证书安全性<br /> </li>
     <li>Adobe策略服务器</li>
    </ul> <p>它是一个可选参数。</p> </td>
  </tr>
  <tr>
   <td>settingsDoc</td>
   <td>该文件包含生成PDF文档时应用的设置(如优化PDF文档以实现Web视图)以及创建PDF文档后应用的设置（如初始视图和安全性）。 它是一个可选参数。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>该文件包含应用于生成的PDF文档的元数据信息。 此参数是可选的。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码将支持文件类型的文档转换为PDF文档。

```java
@Reference GeneratePDFService generatePdfService;
File createPDF(File inputFile, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = generatePdfService.createPDF(inDoc, inputFilename, fileTypeSettings, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

#### exportPDF {#exportpdf}

将PDF文档转换为支持的文件类型。 方法接受PDF作为输入，并以指定的文件类型格式导出PDF的内容。

createPDF服务会返回一个包含结果的java.util.Map。 映射的键为：

* ConvertedDoc：它包含输出文档。

createPDF服务引发以下异常：

* ConversionException
* InvalidParameterException
* FileFormatNotSupportException

**语法：**

```java
Map exportPDF(Document inputDoc, String inputFileName, String formatType, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 输入参数 {#input-parameters-8}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>指定要转换的文档。 </td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>文件的名称以及扩展名。<br /> </td>
  </tr>
  <tr>
   <td>格式类型</td>
   <td>exportPDF API的输出文件格式。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>该文件包含在生成输出文档时要应用的配置。 通常，它是一个XML文件。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例将PDF文档转换为指定的文件类型。

```java
(tx == null)
OSGiUtils.getTransactionManager().begin();
String outputFolder="C:/Output"
Document convertedDoc = null;
Document inDoc = null;
Document settingsDoc = null;
try
{
 inDoc = new Document(inputFile);
 if(inputFileName == null || inputFileName.trim().equals("")) {
  throw new Exception("Input file name cannot be null");
 }
 if(inputFileExtension.lastIndexOf('.') == -1) {
  throw new Exception("Input file should have an extension");
 }
 if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
 settingsDoc = new Document(settingsFile);
 Map result = generatePdfService.exportPDF(inDoc, inputFileName, formatType, settingsDoc);
 convertedDoc = (Document)result.get("ConvertedDoc");
 OSGiUtils.getTransactionManager().commit();
 File outputFile = new File(outputFolder,"OutputFile");
 doc.copyToFile(outputFile);
 return outputFile;
}
catch (Exception e)
{
 if (OSGiUtils.getTransactionManager().getTransaction() != null)
 OSGiUtils.getTransactionManager().rollback();
 throw e;
}
finally {
 if (convertedDoc != null) {
  convertedDoc.dispose();
  convertedDoc = null;
 }
 if (inDoc != null) {
  inDoc.dispose();
  inDoc = null;
 }
 if (settingsDoc != null) {
  settingsDoc.dispose();
  settingsDoc = null;
 }
}
}
```

#### optimizePDF {#optimizepdf}

OptimizePDF API通过减小PDF文件的大小来优化这些文件。 此转换的结果是PDF文件可能小于其原始版本。 此操作还将PDF文档转换为在优化参数中指定的PDF版本。 它会返回包含优化的PDF的OptimizePDFResult对象。

createPDF服务引发以下异常：

* ConversionException
* InvalidParameterException
* FileFormatNotSupportException

**语法：**

```java
OptimizePDFResult optimizePDF(Document inputDoc, String fileTypeSettings, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 输入参数 {#input-parameters-9}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>指定输入文档。 它是必需参数。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>它是一个可选参数。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>该文件包含生成PDF文档时应用的设置(如优化PDF文档以实现Web视图)以及创建PDF文档后应用的设置（如初始视图和安全性）。 它是一个可选参数。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例通过减小输入PDF文件的大小来优化该文件。

```java
@Reference GeneratePDFService generatePdfService;
File optimizePDF(File inputFile, String fileTypeSettings, File settingsFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  OptimizePDFResult result = generatePdfService.optimizePDF(inDoc, fileTypeSettings, settingsDoc);
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

#### htmlToPdf2 {#htmltopdf}

将HTML页面转换为PDF文档。 它接受HTML页面的URL作为输入。

htmlToPdf2服务返回HtmlToPdfResult对象。 您可以通过result.getConvertedDocument()获取转换后的PDF。

htmlToPdf2服务引发以下异常：

* ConversionException
* InvalidParameterException
* FileFormatNotSupportException

**语法：**

```java
HtmlToPdfResult htmlToPdf2(String inputUrl, String fileTypeSettingsName, String securitySettingsName, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 输入参数 {#input-parameters-10}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>指定输入文档。 它是必需参数。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>它是一个可选参数。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>该文件包含生成PDF文档时应用的设置(如优化PDF文档以实现Web视图)以及创建PDF文档后应用的设置（如初始视图和安全性）。 它是一个可选参数。<br /> </td>
  </tr>
 </tbody>
</table>

以下Java代码示例将HTML页面转换为PDF文档。

```java
Reference GeneratePDFService generatePdfService;
File htmlToPdf(String inputUrl, String fileTypeSettingsName, String securitySettingsName, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  HtmlToPdfResult result = generatePdfService.htmlToPdf2(inputURL, fileTypeSettingsName, securitySettingsName, settingsDoc, xmpDoc);;
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

### DistillerService {#distillerservice}

Distiller服务将PostScript、Encapsulated PostScript (EPS)和打印机文本文件(PRN)转换为PDF文件。 Distiller服务通常用于将大量打印文档转换为电子文档，如发票和报表。 将文档转换为PDF还允许企业向客户发送文档的纸质版本和电子版本。 支持的文件格式为.ps、.eps和.prn。 该服务支持以下API：

createPDF服务会返回一个包含结果的java.util.Map。 映射的键为：

* ConvertedDoc ：它包含新创建的PDF文档。
* LogDoc ：它包含日志文件。

createPDF服务引发以下异常：

* ConversionException
* InvalidParameterException
* FileFormatNotSupportException

#### createPDF {#createpdf-1}

将支持的格式转换为PDF文档。 方法接受格式为.ps、.eps和.prn的文件作为输入。 您可以将特定安全权限、输出设置和元数据信息应用到输出PDF文档。

**语法：**

```java
Map createPDF(Document inputDoc, String inputFileName, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 输入参数 {#input-parameters-11}

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>指定输入文档。 它是必需参数。</td>
  </tr>
  <tr>
   <td>输入文件名</td>
   <td>指定输入文件的完整名称以及文件的扩展名。 它是必需参数。</td>
  </tr>
  <tr>
   <td>pdf设置</td>
   <td><p>已转换文档的PDF输出设置。 您只能应用以下设置：</p>
    <ul>
     <li>高品质_打印<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>Press_Quality<br /> </li>
     <li>Minimum_File_Size</li>
    </ul> <p>它是一个可选参数。</p> </td>
  </tr>
  <tr>
   <td>安全设置</td>
   <td><p>已转换文档的安全设置。 您可以应用以下设置：</p>
    <ul>
     <li>无安全性</li>
     <li>密码安全性<br /> </li>
     <li>证书安全性<br /> </li>
     <li>Adobe策略服务器</li>
    </ul> <p>它是一个可选参数。</p> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>该文件包含生成PDF文档时应用的设置(如优化PDF文档以实现Web视图)以及创建PDF文档后应用的设置（如初始视图和安全性）。 它是一个可选参数。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>该文件包含所生成PDF文档的元数据信息。 它是一个可选参数。</td>
  </tr>
 </tbody>
</table>

以下Java代码示例将PostScript (PS)、Encapsulated PostScript (EPS)和打印机文本文件(PRN)类型的输入文件转换为PDF文件。

```java
@Reference DistillerService distillerService;
File createPDF(File inputFile, String inputFilename, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = distillerService.createPDF(inDoc, inputFilename, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

### 文档实用程序服务 {#doc-utility-services}

<!-- Document utilities with synchronous APIs help you <!--convert documents from PDF to XDP file format, Clone a PDF, Retrieve PDF properties (Redact), Multiclone PDF, Sanitise PDF for retrieving uninteneded hidden information, and tag PDF documents with lists and paragraphs. Details of each APIs are given below: -->

#### 自动标记PDF文档 {#auto-tag-api}

Auto Tag PDF API通过向文档添加标记来增强PDF辅助功能，从而确保符合辅助功能标准。 这不仅改善了用户体验，还维护了文档之间的准确性和一致性。 自动标记API支持标记以下元素：

* 文本块（段落）
* 一个运算符中的项目符号列表
* 目录（目录）

![自动标记的PDF文档](assets/auto-tag-api.png)

以下Java代码示例演示了如何将PDF文件转换为标记的PDF文档。

**语法**： `Document tag(final Document inDoc)`

**输入参数**

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>提供作为要标记的输入的文档。 它是必需的参数。<br /> </td>
  </tr>
 </tbody>
</table>

```java
@Reference
private PDFUtilityService pdfutilityService;
private static final File outputFolder = new File("C:/Output/");
void tag(File inputFile) throws Exception
{
    Document inDoc = null;
    try
    {
        inDoc = new Document(inputFile);
        if(inputFile.getName().trim().isEmpty()) {
            throw new Exception("Input file name cannot be null");
        }
        String inputFileExtension = "";
        int dotIndex = inputFile.getName().lastIndexOf('.');
        if (dotIndex > 0 && dotIndex < inputFile.getName().length() - 1) {
            inputFileExtension = inputFile.getName().substring(dotIndex + 1);
        }
        if(inputFileExtension.isEmpty()) {
            throw new Exception("Input file should have an extension");
        }
        Document taggedDoc;
        taggedDoc = pdfutilityService.tag(inDoc);
        File outputFile = new File(outputFolder,"Output.pdf");
        taggedDoc.copyToFile(outputFile);
        taggedDoc.close();
    } 
    finally {
        if (inDoc != null) {
            inDoc.dispose();
            inDoc = null;
        }
    }
}
```
