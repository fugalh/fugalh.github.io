---
layout: post
status: publish
published: true
title: RTDX OLE API
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
excerpt: <p>And now, ladies and gentlemen, I will answer the questions you have been
  dying to have answered! Right before your very eyes I will demystify The Texas Instruments
  TMS320C6416DSK RTDX OLE API!</p>
wordpress_id: 123
wordpress_url: urn:uuid:6df96e4d-6290-43b3-a5df-879cd047c04d
date: 2006-05-04 20:28:00.000000000 -07:00
tags:
- audio
- cs
- ruby
- dsp
- win32ole
- rtdx
- ti
- TMS320C6416DSK
- c6xx
comments: []
---
<p>And now, ladies and gentlemen, I will answer the questions you have been dying to have answered! Right before your very eyes I will demystify The Texas Instruments TMS320C6416DSK RTDX OLE API!</p><a id="more"></a><a id="more-123"></a><p>Ok, so most of you don't care. I'm putting it on the web for posterity's sake, because it's dreadfully impossible to find. I'm no OLE expert and maybe everyone that wants to do OLE just uses some OLE browser built into Visual Studio or something, but I'm too lazy to install the copy of Visual Studio I won in a programming contest (hey, getting me to use Windows at all is a feat).</p>

<p>I wrote a nifty little ruby script to dump what I believe is probably the relevant info:</p>

<div class="typocode"><pre><code class="typocode_ruby ">    <span class="ident">require</span> <span class="punct">'</span><span class="string">win32ole</span><span class="punct">'</span>
    <span class="ident">rtdx</span> <span class="punct">=</span> <span class="constant">WIN32OLE</span><span class="punct">.</span><span class="ident">new</span><span class="punct">('</span><span class="string">RTDX</span><span class="punct">')</span>
    <span class="ident">rtdx</span><span class="punct">.</span><span class="ident">ole_methods</span><span class="punct">.</span><span class="ident">each</span> <span class="keyword">do</span> <span class="punct">|</span><span class="ident">m</span><span class="punct">|</span>
      <span class="ident">print</span> <span class="punct">&quot;</span><span class="string"><span class="expr">#{m.return_type}</span><span class="escape">\t</span><span class="expr">#{m}</span>(</span><span class="punct">&quot;</span>
      <span class="ident">print</span> <span class="ident">m</span><span class="punct">.</span><span class="ident">params</span><span class="punct">.</span><span class="ident">collect</span><span class="punct">{|</span><span class="ident">p</span><span class="punct">|</span>
        <span class="punct">&quot;</span><span class="string"><span class="expr">#{p.ole_type}</span> <span class="expr">#{p}</span></span><span class="punct">&quot;</span> <span class="punct">+</span>
        <span class="keyword">if</span> <span class="ident">p</span><span class="punct">.</span><span class="ident">default</span>
          <span class="punct">&quot;</span><span class="string">=<span class="expr">#{p.default}</span></span><span class="punct">&quot;</span>
        <span class="keyword">else</span>
          <span class="punct">&quot;</span><span class="string"></span><span class="punct">&quot;</span>
         <span class="keyword">end</span>
       <span class="punct">}.</span><span class="ident">join</span><span class="punct">(&quot;</span><span class="string">, </span><span class="punct">&quot;)</span>
      <span class="ident">puts</span> <span class="punct">&quot;</span><span class="string">)</span><span class="punct">&quot;</span>
    <span class="keyword">end</span></code></pre></div>

<p>And here is the result:</p>

<pre><code>VOID  QueryInterface(GUID riid, VOID,VOID ppvObj)
UI4  AddRef()
UI4  Release()
VOID  GetTypeInfoCount(UINT pctinfo)
VOID  GetTypeInfo(UINT itinfo, UI4 lcid, VOID,VOID pptinfo)
VOID  GetIDsOfNames(GUID riid, I1,I1 rgszNames, UINT cNames, UI4 lcid, I4 rgdispid)
VOID  Invoke(I4 dispidMember, GUID riid, UI4 lcid, UI2 wFlags, DISPPARAMS pdispparams, VARIANT pvarResult, EXCEPINFO pexcepinfo, UINT puArgErr)
I4  Open(BSTR Channel_String, BSTR Read_Write)
I4  Close()
I4  Read(VARIANT pArr, I4 dataType, I4 numBytes)
I4  ReadI1(UI1 pData)
I4  ReadI2(I2 pData)
I4  ReadI4(I4 pData)
I4  ReadF4(R4 pData)
I4  ReadF8(R8 pData)
I4  ReadSAI1(VARIANT pArr)
I4  ReadSAI2(VARIANT pArr)
I4  ReadSAI4(VARIANT pArr)
I4  ReadSAF4(VARIANT pArr)
I4  ReadSAF8(VARIANT pArr)
VARIANT  ReadSAI2V(I4 pStatus)
VARIANT  ReadSAI4V(I4 pStatus)
I4  WriteI1(UI1 Data, I4 numBytes)
I4  WriteI2(I2 Data, I4 numBytes)
I4  WriteI4(I4 Data, I4 numBytes)
I4  WriteF4(R4 Data, I4 numBytes)
I4  WriteF8(R8 Data, I4 numBytes)
I4  Write(VARIANT Arr, I4 numBytes)
I4  Rewind()
I4  Flush()
I4  Seek(I4 MsgNum)
I4  SeekData(I4 numBytes)
I4  StatusOfWrite(I4 numBytes)
I4  GetNumMsgs(I4 pNum)
I4  GetChannelID(BSTR Channel_String, I4 chanId)
I4  GotoNextMsg()
I4  GetMsgID(I4 pMsgId)
I4  GetMsgNumber(I4 pMsgNum)
I4  GetMsgLength(I4 pLength)
I4  EnableRtdx()
I4  DisableRtdx()
I4  EnableChannel(BSTR ChannelName)
I4  DisableChannel(BSTR ChannelName)
I4  GetChannelStatus(BSTR ChannelName, I4 pChannelStatus)
I4  ConfigureRtdx(I2 Mode, I4 MainBufferSize, I4 NumOfMainBuffers)
I4  ConfigureLogFile(BSTR FileName, I4 FileSize, I2 FileFullMode, I2 FileOpenMode)
I4  GetRTDXRev(I4 RevNum)
I4  GetStatusString(BSTR StatusString)
I4  GetCapability(I4 Capability)
I4  RunDiagnostics(I2 TestType, I4 TestMode, I4 TestInfo)
BSTR  GetDiagFilePath(I2 TestType)
I4  SetProcessor(BSTR Board, BSTR Cpu)
HRESULT  GetTypeInfoCount(UINT pctinfo)
HRESULT  GetTypeInfo(UINT itinfo, UI4 lcid, VOID,VOID pptinfo)
HRESULT  GetIDsOfNames(GUID riid, I1,I1 rgszNames, UINT cNames, UI4 lcid, I4 rgdispid)
HRESULT  Invoke(I4 dispidMember, GUID riid, UI4 lcid, UI2 wFlags, DISPPARAMS pdispparams, VARIANT pvarResult, EXCEPINFO pexcepinfo, UINT puArgErr)
</code></pre>
