.NET Core Hosting Sample
========================

This sample demonstrates a simple .NET Core host using the hosting APIs from [`coreclrhost.h`](https://github.com/dotnet/coreclr/blob/main/src/coreclr/hosts/inc/coreclrhost.h). The sample host loads and starts the .NET runtime, loads managed code, calls into a managed method, and provides a function pointer for the managed code to call back into the host.

This sample is part of the [.NET Core hosting tutorial](https://docs.microsoft.com/dotnet/core/tutorials/netcore-hosting). See that topic for a more detailed explanation of this sample.

About .NET Core Hosts
---------------------

.NET Core applications are always run by a host. In most cases, the default dotnet.exe host is used.

It is possible to create your own host, though, to enable starting and running .NET Core code from a native application, or to enable a high degree of control over how the runtime operates. More complex, real-world hosts can be found in the [dotnet/coreclr](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts) repository.

Build and Run
-------------

To build this sample, just use the included build scripts *build.bat*, *build.sh*, or *buildOsx.sh*. These scripts build both the managed target assembly (ManagedLibrary.dll) and the host (SampleHost.exe). The build scripts are just simple wrappers around two build calls (`dotnet publish` for the managed component of the sample and cl.exe/g++ for the host), so it's also easy to build the two components directly if you prefer. The build scripts build for Windows 10 (x64), Linux (x64), and OSX (x64), respectively, and assume that both the dotnet CLI and the C++ compiler (cl.exe or g++) are available on the path. On Windows, a [Developer Command Prompt for Visual Studio](https://docs.microsoft.com/cpp/build/building-on-the-command-line#developer_command_prompt_shortcuts) should be used. The build scripts will need modified if you intend to target other platforms or use tools from other paths. Be sure that the bitness of the host and sample app match. By default, the build scripts build ManagedLibrary.dll for x64, so you will need to build the host for 64-bit.

To run the host, just execute SampleHost from the bin/{{OS}} directory.

bin/linux
-----------------------------------

<pre>
[ernad.husremovic@sa.out.ba@zvijer linux]$ ls
createdump                                         System.Net.Ping.dll
libclrjit.so                                       System.Net.Primitives.dll
libcoreclr.so                                      System.Net.Requests.dll
libcoreclrtraceptprovider.so                       System.Net.Security.dll
libdbgshim.so                                      System.Net.ServicePoint.dll
libhostfxr.so                                      System.Net.Sockets.dll
libhostpolicy.so                                   System.Net.WebClient.dll
libmscordaccore.so                                 System.Net.WebHeaderCollection.dll
libmscordbi.so                                     System.Net.WebProxy.dll
libSystem.IO.Compression.Native.a                  System.Net.WebSockets.Client.dll
libSystem.IO.Compression.Native.so                 System.Net.WebSockets.dll
libSystem.Native.a                                 System.Numerics.dll
libSystem.Native.so                                System.Numerics.Vectors.dll
libSystem.Net.Security.Native.a                    System.ObjectModel.dll
libSystem.Net.Security.Native.so                   System.Private.CoreLib.dll
libSystem.Security.Cryptography.Native.OpenSsl.a   System.Private.DataContractSerialization.dll
libSystem.Security.Cryptography.Native.OpenSsl.so  System.Private.Uri.dll
ManagedLibrary                                     System.Private.Xml.dll
ManagedLibrary.deps.json                           System.Private.Xml.Linq.dll
ManagedLibrary.dll                                 System.Reflection.DispatchProxy.dll
ManagedLibrary.pdb                                 System.Reflection.dll
ManagedLibrary.runtimeconfig.json                  System.Reflection.Emit.dll
Microsoft.CSharp.dll                               System.Reflection.Emit.ILGeneration.dll
Microsoft.VisualBasic.Core.dll                     System.Reflection.Emit.Lightweight.dll
Microsoft.VisualBasic.dll                          System.Reflection.Extensions.dll
Microsoft.Win32.Primitives.dll                     System.Reflection.Metadata.dll
Microsoft.Win32.Registry.dll                       System.Reflection.Primitives.dll
mscorlib.dll                                       System.Reflection.TypeExtensions.dll
netstandard.dll                                    System.Resources.Reader.dll
SampleHost                                         System.Resources.ResourceManager.dll
System.AppContext.dll                              System.Resources.Writer.dll
System.Buffers.dll                                 System.Runtime.CompilerServices.Unsafe.dll
System.Collections.Concurrent.dll                  System.Runtime.CompilerServices.VisualC.dll
System.Collections.dll                             System.Runtime.dll
System.Collections.Immutable.dll                   System.Runtime.Extensions.dll
System.Collections.NonGeneric.dll                  System.Runtime.Handles.dll
System.Collections.Specialized.dll                 System.Runtime.InteropServices.dll
System.ComponentModel.Annotations.dll              System.Runtime.InteropServices.RuntimeInformation.dll
System.ComponentModel.DataAnnotations.dll          System.Runtime.Intrinsics.dll
System.ComponentModel.dll                          System.Runtime.Loader.dll
System.ComponentModel.EventBasedAsync.dll          System.Runtime.Numerics.dll
System.ComponentModel.Primitives.dll               System.Runtime.Serialization.dll
System.ComponentModel.TypeConverter.dll            System.Runtime.Serialization.Formatters.dll
System.Configuration.dll                           System.Runtime.Serialization.Json.dll
System.Console.dll                                 System.Runtime.Serialization.Primitives.dll
System.Core.dll                                    System.Runtime.Serialization.Xml.dll
System.Data.Common.dll                             System.Security.AccessControl.dll
System.Data.DataSetExtensions.dll                  System.Security.Claims.dll
System.Data.dll                                    System.Security.Cryptography.Algorithms.dll
System.Diagnostics.Contracts.dll                   System.Security.Cryptography.Cng.dll
System.Diagnostics.Debug.dll                       System.Security.Cryptography.Csp.dll
System.Diagnostics.DiagnosticSource.dll            System.Security.Cryptography.Encoding.dll
System.Diagnostics.FileVersionInfo.dll             System.Security.Cryptography.OpenSsl.dll
System.Diagnostics.Process.dll                     System.Security.Cryptography.Primitives.dll
System.Diagnostics.StackTrace.dll                  System.Security.Cryptography.X509Certificates.dll
System.Diagnostics.TextWriterTraceListener.dll     System.Security.dll
System.Diagnostics.Tools.dll                       System.Security.Principal.dll
System.Diagnostics.TraceSource.dll                 System.Security.Principal.Windows.dll
System.Diagnostics.Tracing.dll                     System.Security.SecureString.dll
System.dll                                         System.ServiceModel.Web.dll
System.Drawing.dll                                 System.ServiceProcess.dll
System.Drawing.Primitives.dll                      System.Text.Encoding.CodePages.dll
System.Dynamic.Runtime.dll                         System.Text.Encoding.dll
System.Formats.Asn1.dll                            System.Text.Encoding.Extensions.dll
System.Globalization.Calendars.dll                 System.Text.Encodings.Web.dll
System.Globalization.dll                           System.Text.Json.dll
System.Globalization.Extensions.dll                System.Text.RegularExpressions.dll
System.IO.Compression.Brotli.dll                   System.Threading.Channels.dll
System.IO.Compression.dll                          System.Threading.dll
System.IO.Compression.FileSystem.dll               System.Threading.Overlapped.dll
System.IO.Compression.ZipFile.dll                  System.Threading.Tasks.Dataflow.dll
System.IO.dll                                      System.Threading.Tasks.dll
System.IO.FileSystem.AccessControl.dll             System.Threading.Tasks.Extensions.dll
System.IO.FileSystem.dll                           System.Threading.Tasks.Parallel.dll
System.IO.FileSystem.DriveInfo.dll                 System.Threading.Thread.dll
System.IO.FileSystem.Primitives.dll                System.Threading.ThreadPool.dll
System.IO.FileSystem.Watcher.dll                   System.Threading.Timer.dll
System.IO.IsolatedStorage.dll                      System.Transactions.dll
System.IO.MemoryMappedFiles.dll                    System.Transactions.Local.dll
System.IO.Pipes.AccessControl.dll                  System.ValueTuple.dll
System.IO.Pipes.dll                                System.Web.dll
System.IO.UnmanagedMemoryStream.dll                System.Web.HttpUtility.dll
System.Linq.dll                                    System.Windows.dll
System.Linq.Expressions.dll                        System.Xml.dll
System.Linq.Parallel.dll                           System.Xml.Linq.dll
System.Linq.Queryable.dll                          System.Xml.ReaderWriter.dll
System.Memory.dll                                  System.Xml.Serialization.dll
System.Net.dll                                     System.Xml.XDocument.dll
System.Net.Http.dll                                System.Xml.XmlDocument.dll
System.Net.Http.Json.dll                           System.Xml.XmlSerializer.dll
System.Net.HttpListener.dll                        System.Xml.XPath.dll
System.Net.Mail.dll                                System.Xml.XPath.XDocument.dll
System.Net.NameResolution.dll                      WindowsBase.dll
System.Net.NetworkInformation.dll
</pre>

<pre>
[ernad.husremovic@sa.out.ba@zvijer linux]$ du -sh .
73M	.
</pre>

Run linux sample
---------------------------

<pre>
[ernad.husremovic@sa.out.ba@zvijer linux]$ ./SampleHost

Loaded CoreCLR from /home/ernad.husremovic/dotnet/samples/core/hosting/HostWithCoreClrHost/bin/linux/libcoreclr.so
==== CoreCLR started ====
Managed delegate created
.NET Version: 5.0.6
Beginning work iteration 1
[NATIVE] Received status from managed code: 1
Received response [-1] from progress function
.NET Version: 5.0.6
Beginning work iteration 2
[NATIVE] Received status from managed code: 2
Received response [-2] from progress function
.NET Version: 5.0.6
Beginning work iteration 3
[NATIVE] Received status from managed code: 3
Received response [-3] from progress function
.NET Version: 5.0.6
Beginning work iteration 4
[NATIVE] Received status from managed code: 4
Received response [-4] from progress function
.NET Version: 5.0.6
Beginning work iteration 5
[NATIVE] Received status from managed code: 5
Received response [-5] from progress function
Work completed
Managed code returned: Data received: 0, 0.25, 0.5, 0.75
CoreCLR successfully shutdown
</pre>
