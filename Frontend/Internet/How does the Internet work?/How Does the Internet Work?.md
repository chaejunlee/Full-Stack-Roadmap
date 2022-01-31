# How Does the Internet Work?

Source: [How Does the Internet Work?](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

## Introduction

- 인터넷을 가능케하는 기저 인프라와 기술을 알아봄.
- 컴퓨터 네트워크 미니 렉쳐;;

## Internet Address

- 인터넷에 연결된 모든 컴퓨터는 **반드시** 고유한 address를 가지고 있어야 함.
- 인터넷 address는 **nnn.nnn.nnn.nnn** 처럼 생김(nnn은 0~255의 숫자임).
- 이 address는 IP(Internet Procotol) address라고도 불림.
- 두 개의 컴퓨터는 인터넷을 통해 연결됨.
    - Internet Service Provider(ISP)를 통해 인터넷에 연결하게 되면 dial-in session 간 임시 IP address를 받게됨.
    - Local Area Network(LAN)을 통해 인터넷에 연결하게 되면 해당 컴퓨터는 고정된 IP를 가지거나 DHCP(Dynamic Host Configuration Protocol) 서버를 통해 임시 IP를 할당 받을 수 있다.
    - 어쨋든 인터넷에 연결하려면 컴퓨터는 고유한 IP address를 가져야 함.

## Protocol Stacks and Packets

- 네 컴퓨터는 인터넷에 연결돼있고 고유한 IP를 가지고 있음. 인터넷에 연결된 다른 컴퓨터와는 어떻게 메시지를 주고 받을까?
- 메시지를 문자 텍스트로 바꾸고, 전기 신호로 바꾸고, 인터넷으로 보내고, 다시 문자 텍스트로 변환하는 과정이 필요함.
- 이 과정은 **Protocol Stack**을 통해서 이루어짐.
- 모든 컴퓨터는 인터넷으로 통신하기 위해 프로토콜 스택이 필요함. OS 차원에서 프로토콜 스택이 구현돼있음.
- 인터넷이 사용하는 프로토콜 스택은 두 개의 통신 프로토콜인 TCP/IP임.

<table cellpadding="8" border="1">
    <tbody>
        <tr>
            <th>Protocol Layer</th>
            <th>Comments</th>
        </tr>
        <tr>
            <td>Application Protocols Layer</td>
            <td>Protocols specific to applications such as WWW, e-mail, FTP, etc.</td>
        </tr>
        <tr>
            <td>Transmission Control Protocol Layer</td>
            <td>TCP directs packets to a specific application on a computer using a port number.</td>
        </tr>
        <tr>
            <td>Internet Protocol Layer</td>
            <td>IP directs packets to a specific computer using an IP address.</td>
        </tr>
        <tr>
            <td>Hardware Layer</td>
            <td>Converts binary packet data to network signals and back.
                <br>
                (E.g. ethernet network card, modem for phone lines, etc.)
            </td>
        </tr>
    </tbody>
</table>

![Diagram 2 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e394acc7-de85-4b76-b801-0a4279b19e97/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220130T131940Z&X-Amz-Expires=86400&X-Amz-Signature=66eaf0ff897fe75268ff9efb7559e23de7c699897968312914d18fa273ab0d17&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 2 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

### 컴퓨터 A에서 컴퓨터 B로 메시지를 보내는 절차

1. 메시지는 컴퓨터의 프로토콜 스택의 위 계층에서부터 시작해서 아래 계층으로 내려간다.
2. 보내려는 메시지가 길다면 메시지는 작은 단위의 데이터로 쪼개지기도 한다. 인터넷으로 보내지는 데이터는 관리 가능한 단위로 나뉘어 보내지기 때문이다. 이러한 단위의 데이터를 **패킷**이라고 한다.
3. 패킷은 응용 계층(Application Layer)을 지나 TCP 계층으로 이동한다. 이 때, 각 패킷에 **포트 넘버**가 할당된다. (대부분의 프로그램은 TCP/IP 스택을 통해 메시지를 보낸다. 우리는 메시지를 받을 목적지 컴퓨터의 프로그램을 알아야 한다. 그 프로그램은 특정 포트에서 수신 대기할 것이기 때문이다.)
4. TCP 계층을 지난 패킷은 IP 계층으로 이동한다. 패킷이 IP 계층으로 이동할 때, 각 패킷은 목적지의 IP 주소를 받는다.
5. 포트 넘버와 IP 주소를 가지고 있는 메시지 패킷은 이제 인터넷으로 보낼 수 있다. 메시지의 텍스트를 포함하는 패킷을 전자 신호로 변환하고 전화선을 통해 전송하는 작업은 하드웨어 계층이 알아서 처리한다.
6. 전화선의 다른 끝 쪽에 있는 ISP는 인터넷에 직접적으로 연결되어있다. ISP 라우터는 각 패킷의 목적지 주소를 검사하고 보낼 위치를 결정한다. 라우터에서 나온 패킷의 다음 단계는 대부분 또 다른 라우터다.
7. 그러다 결국 패킷은 목적지 컴퓨터에 도착한다. 여기서 패킷은 목적지 컴퓨터의 TCP/IP 스택 맨 아래에서부터 위로 이동한다.
8. 패킷이 스택을 따라 위로 이동하면서 컴퓨터의 스택이 추가한 모든 라우팅 데이터는 패킷에서부터 제거된다.
9. 데이터가 스택의 맨 위에 도달하면 패킷은 원래 형태로 재조립된다.

## Networking Infrastructure

패킷이 인터넷을 통해 컴퓨터에서 컴퓨터로 어떻게 보내지는지 알아보았다. 그렇다면 인터넷을 어떻게 구성돼있을까?

![Diagram 3 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/60a2c10c-30b2-478c-90bb-ed096fe203f9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220130T132004Z&X-Amz-Expires=86400&X-Amz-Signature=2642246550b06cc4c047aeb2049d6a9f938645be5bdb3d457a0a90dfd9d5c13b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 3 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

ISP는 전화 접속(dial-in) 고객을 위해 모뎀 풀을 유지 관리한다. 모뎀 풀은 ****모뎀 풀에서 백본 (backbone, 초고속 통신망) 또는 전용 회선 라우터로의 데이터 흐름을 제어하는 일종의 컴퓨터(보통 전용 컴퓨터)에 의해 관리된다. 이러한 셋업은 네트워크에 대한 액세스를 '제공(serve)'하므로 포트 서버라고도 한다. 일반적으로 청구 및 사용 정보도 여기에 수집된다.

패킷이 전화 네트워크와 ISP의 로컬 장비를 통과한 후 패킷은 ISP의 백본 또는 ISP가 구입한 대역폭 백본으로 라우팅된다. 여기에서 패킷은 목적지인 컴퓨터를 찾을 때까지 일반적으로 여러 라우터와 여러 백본, 전용 회선 및 기타 네트워크를 통해 이동합니다.

`tracert` 나 `traceroute` 명령어를 통해 패킷이 인터넷을 타고 간 정확한 루트를 확인할 수 있다.

## Internet Infrastructure

인터넷 백본(초고속 통신망)은 서로 연결된 매우 큰 네트워크들로 이루어져 있다. 이러한 큰 네트워크들을 **Network Service Provider(NSP)**라고 부른다. 규모 있는 NSP들로 UUNet, CerfNet, IBM, BBN Planet, SprintNet, PSINet 등이 있다. 이러한 네트워크는 서로 피어링하여 패킷 트래픽을 교환한다. 각 NSP는 3개의 **Network Access Points(NAP)**에 연결돼있어야 한다. NAP에서 패킷 트래픽은 한 NSP의 백본에서 다른 NSP의 백본으로 점프할 수 있다. NSP는 또한 **Metropolitan Area Exchange(MAE)**와도 서로 연결돼있다. MAE는 NAP와 같은 역할을 하지만 개인의 소유이다. NAP와 MAE는 **IX(**Internet Exchange Points)라고 불린다. NSP는 ISP나 소규모 대역폭 제공자 같은 소규모 네트워크에 대역폭을 팔기도 한다. 아래 그림은 계층적 인프라를 보여준다.

![Diagram 4 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ec20ce89-8651-4fb8-9cfc-1665b2283aa2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220130T132031Z&X-Amz-Expires=86400&X-Amz-Signature=fed6d2b0fc18ab05e5788eeaa027dc4865fd2d6be2d100f81b65135e7000e663&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 4 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

위 다이어그램에는 생략된 부분이 많이 있다. 위 다이어그램은 NSP가 자기들끼리, 그리고 작은 ISP들과 상호 연결될 수 있음을 보여주기 위한 다이어그램이다. 물리적 네트워크 구성 요소가 표현되어있지 않은 것을 볼 수 있다. NSP 백본 인프라 하나 그리기에도 너무 복잡하기 때문이다. 인터넷의 실제 지도를 그리는 것은 인터넷의 크기, 복잡성 및 끊임없이 변화하는 구조로 인해 거의 불가능하다.

## The Internet Routing Hierarchy

패킷은 어떻게 인터넷에서 자기 갈 길을 찾는가? 어떤 컴퓨터라도 다른 컴퓨터의 위치를 알고 있지 않고 패킷이 모든 컴퓨터에 보내지는 것도 아니다. 패킷을 목적지로 보내기 위해 필요한 정보가 저장된 라우팅 테이블은 인터넷과 연결된 라우터에 저장돼있다.

**라우터는 패킷 스위치다.** 라우터는 패킷을 다른 네크워크로 보내기 위해 네트워크들 사이에 연결돼있다. 각 라우터는 연결된 서브 네트워크들에 대한 IP 주소 등의 정보를 알고 있다. 라우터는 자신 ‘위’의 IP까지 알고 있지는 않다. 백본에 연결된 검은 박스는 라우터다. 맨 위에 있는 대규모 NSP들은 NAP에서 연결된다. 그 아래에는 작은 서브 네트워크가 있고 그 아래에도 서브 네트워크가 더 있다. 맨 아래에는 컴퓨터와 연결된 2개의 LAN(Local Area Network)가 있다.

![Diagram 5 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c409dcba-e32d-4ceb-a1ae-50770be897ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220130T132058Z&X-Amz-Expires=86400&X-Amz-Signature=338dae27b2ef869cd1c020fdb7334fa8d73aff27c8836e4aad016996af773a06&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 5 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

라우터는 라우터에 도착한 패킷의 발신 컴퓨터의 IP 계층에서 넣은 IP 주소를 확인한다. 라우터는 라우팅 테이블을 확인한다. 라우터는 IP 주소를 가지고 있는 네트워크를 찾으면 패킷을 해당 네트워크로 보낸다. IP 주소를 가지고 있는 네트워크를 찾지 못하면 라우터는 기본 루트로 패킷을 보낸다. 기본 루트는 백본 계층 상의 윗 방향의 다음 라우터로 보내는 것이다. NSP 백본까지 위쪽으로 패킷을 라우팅하며 패킷을 보낼 곳을 아는 라우터를 찾는다. NSP 백본에 연결된 라우터는 가장 큰 라우팅 테이블을 가지고 있다. 패킷은 NSP 백본에서 올바른 백본으로 라우팅된다. 올바른 백본으로 라우팅된 패킷은 목적지까지 아랫 방향의 작은 네트워크들로 내려간다.

## Domain Names and Address Resolution

접속하려는 컴퓨터의 IP 주소를 모른다면 어떻게 할까? *[www.anothercomputer.com](http://www.anothercomputer.com)* 같은 사이트는 어떻게 접속할까? 웹 브라우저는 DNS(Domain Name Service)를 통해 컴퓨터의 IP 주소를 알아낸다. DNS는 컴퓨터의 이름과 그에 대응되는 IP 주소를 추적하는 분산된 데이터베이스이다.

인터넷에 연결된 많은 컴퓨터들은 DNS 데이터베이스의 일부분과 다른 컴퓨터가 이를 접근할 수 있게 해주는 소프트웨어를 호스트한다. 이런 컴퓨터를 DNS 서버라고 부른다. DNS 서버는 DNS DB의 일부만을 가지고 있다. DNS  DB 전체를 가지고 있는 DNS 서버는 없다. 다른 컴퓨터가 요청한 도메인 네임이 DNS 서버에 없다면 그 DNS 서버는 요청하는 컴퓨터를 다른 DNS 서버로 리다이렉트한다.

![Diagram 6 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/75a78df0-742b-454a-b1dc-34a399d559e1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220130%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220130T132121Z&X-Amz-Expires=86400&X-Amz-Signature=1780596e76b52615504c0163b7db12ef01644fe97a63240f78c6b70885bbd4c7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 6 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

DNS는 IP 라우팅 계층과 비슷한 계층으로 설계돼있다.

DNS는 IP 라우팅 계층과 비슷한 계층으로 설계돼있다. 이름 확인(name resolution)을 요청하는 컴퓨터는 요청하는 도메인 네임을 확인할 수 있는 DNS 서버를 찾을 때까지 계층 구조의 '윗 방향'으로 리다이렉트된다. Diagram 6은 계층 구조의 일부를 보여준다. 트리의 맨 위는 도메인 루트들이다. 더 오래되고 일반적인 도메인 중 일부는 상단 주변에 위치해있다. 표시되지 않은 전 세계의 수많은 DNS 서버들이 나머지 계층 구조를 형성한다.

인터넷 연결이 설정(윈도우의 LAN이나 Dial-Up 네트워크)될 때 하나의 기본 DNS 서버와 하나 이상의 보조 DNS 서버도 같이 설치된다. 이렇게 하면 도메인 이름 확인이 필요한 모든 인터넷 응용 프로그램이 올바르게 작동할 수 있다. 예를 들어, 웹 브라우저에 웹 주소를 입력하면 브라우저는 먼저 기본 DNS 서버에 연결한다. 입력한 도메인 이름에 대한 IP 주소를 얻은 브라우저는 목표 컴퓨터에 연결하여 원하는 웹 페이지를 요청합니다.

## Internet Protocols Revisited

프로토콜 스택에서 언급했듯, 인터넷에서는 다양한 프로토콜이 사용되고 있음을 추측할 수 있다. 인터넷이 작동되기 위해서 많은 통신 프로토콜이 필요하다. TCP/IP 프로토콜과 라우팅 프로토콜, 미디어 액세스 컨트롤 프토로콜, 어플리케이션 레벨 프로토콜 등이 필요하다. 프로토콜을 High Level Protocol에서부터 Low Level Protocol까지 한번 알아보겠다.

## Application Protocols: HTTP and the World Wide Web

인터넷에서 가장 많이 쓰이는 서비스는 World Wide Web(WWW)이다. 웹을 작동시키는 어플리케이션 프로토콜은 Hypertext Transfer Protocol(HTTP)이다. 웹 페이지를 작성하는데 쓰이는 HTML(Hypertext Markup Language)와는 다르다. HTTP는 웹 브라우저와 웹 서버가 인터넷에서 서로와 통신하기 위해 사용하는 프로토콜이다. HTTP는  어플리케이션 레벨의 프로토콜인데 프로토콜 스택에서 TCP 계층 위에 놓여있기 때문이다. HTTP는 특정 어플리케이션이 다른 어플리케이션과 통신하기 위해 사용된다. 어플리케이션에는 웹 브라우저와 웹 서버 등이 있다.

HTTP는 비연결형 텍스트 기반 프로토콜이다. 웹 브라우저 같은 클라이언트는 웹 페이지나 이미지 같은 웹 요소들을 웹 서버에게 요청(request)한다. 서버가 요청을 전달(처리, service)하고 나면 인터넷을 통한 클라이언트와 서버의 연결은 끊어진다. 연결은 각 요청마다 새롭게 다시해야 한다. 대부분의 프로토콜들은 연결 지향적이다. 통신하고 있는 두 컴퓨터는 인터넷을 통한 연결을 열어두는 것을 의미한다. 하지만 HTTP는 다르다. 서버에 새로 연결한 뒤에 클라이언트는 HTTP 요청을 보낼 수 있다.

→ HTTP는 먼저 연결하고 request를 보낼 수 있다. 연결은 request마다 새로 해야한다.

URL을 웹 브라우저에 입력했을 때 다음이 일어난다.

1. URL이 도메인 네임을 포함한다면 브라우저는 도메인 네임 서버에 먼저 연결한다. 그 후 도메인 네임 서버에서 웹 서버의 IP 주소를 받아온다.
2. 웹 브라우저는 웹 서버에 *연결*한 뒤 원하는 웹페이지에 대한 HTTP *요청*을 프로토콜 스택을 통해 보낸다.
3. 웹 서버는 요청을 받은 뒤 요청하는 페이지를 확인한다. 페이지가 존재한다면 웹 서버는 보내준다. 서버가 요청된 페이지를 찾을 수 없다면 HTTP 404 에러 메시지를 보낸다. (404는 ‘Page Not Found’를 위미한다.)
4. 웹 브라우저는 페이지를 돌려받고 연결은 닫힌다.
5. 브라우저는 페이지를 parse한 뒤 웹 페이지를 완성하기 위해 필요한 다른 페이지 요소를 찾는다. 다른 페이지 요소에는 이미지 애플릿 등이 있다.
6. 필요한 각 요소에 대해 브라우저는 각 요소에 대해 서버에 추가적인 연결을 만든 뒤 HTTP 요청을 수행한다.
7. 브라우저가 모든 이미지, 애플릿 등의 로드가 끝난 뒤 페이지는 브라우저 창에 완전히 로드된다.

대부분의 인터넷 프로토콜은 RFC(Request For Comments)라는 이름의 인터넷 문서로 지정된다. 

## Application Protocols: SMTP and Electronic Mail

일반적으로 쓰이는 또다른 인터넷 서비스는 이메일이다. 이메일은 SMTP(Simple Mail Transfer Protocol)이라는 어플리케이션 레벨 프로토콜을 사용한다. SMTP 역시 문서 기반 프로토콜이다. HTTP와는 다르게 SMTP는 연결 지향적이다. SMTP는 HTTP보다 복잡하다. SMTP에는 HTTP보다 더 많은 명령어과 고려 사항이 있다.

이메일을 읽기 위해 이메일 클라이언트를 열면 다음이 일어난다.

1. 메일 클라이언트는 기본 메일 서버와 연결을 연다. 메일 서버의 IP 주소나 도메인 네임은 일반적으로 메일 클라이언트가 설치될 때 설정된다.
2. 메일 서버는 항상 자신을 식별하기 위한 첫 번째 메시지를 보낸다.
3. 클라이언트는 STMP HELO 명령을 서버 보낸다. 그에 서버는 ‘250 OK’ 메시지로 답할 것이다.
4. 클라이언트가 메일을 확인하는지, 메일을 보내는지 등에 따라 적절한 SMTP 명령이 서버로 보내지고 서버는 그에 따라 응답한다.
5. 이 요청/응답 트랜잭션은 클라이언트가 SMTP QUIT 명령을 보낼 때까지 계속된다. 그러면 서버가 작별 인사를 하고 연결이 닫힌다.

## Transmission Control Protocol

어플리케이션 계층 아래에는 TCP 계층이라는 프로토콜 스택이 존재한다. 어플리케이션이 인터넷을 통해 다른 컴퓨터와 연결하면 특정 어플리케이션 계층 프로토콜을 사용해 보내는 메시지는 TCP 계층으로 전달된다. **TCP는 목적지 컴퓨터의 알맞은 어플리케이션으로 어플리케이션 프로토콜을 라우팅하는 역할을 한다.** 이것을 해내기 위해 포트 넘버가 사용된다. 포트는 각 컴퓨터의 독립된(separate) 채널로 생각될 수 있다. 두 개의 다른 어플리케이션은 다른 포트 넘버를 사용한다. 패킷이 컴퓨터에 도착해서 프로토콜 스택을 올라갈 때, TCP 계층은 패킷의 포트 넘버를 보고 어떤 어플리케이션이 해당 패킷을 받을지 정한다.

TCP는 다음과 같이 동작한다.

- TCP 계층이 위에서부터 어플리케이션 계층 데이터를 받으면 그것을 관리 가능한 ‘청크(chunck)’로 분할한다. 그리고 특정 TCP 정보를 포함된 TCP 헤더를 각 청크에 추가한다. TCP 헤더에 들어있는 정보는 데이터가 보내져야 할 프로그램의 포트 넘버 등이 있다.
- TCP 계층이 아래의 IP 계층으로부터 패킷을 받으면 TCP 계층은 TCP 헤더 데이터를 패킷에서부터 제거한다. 그리고 필요하다면 데이터 복원을 한다. 그리고는 TCP 헤더의 포트 넘버를 사용해 알맞은 어플리케이션으로 데이터를 보낸다.

위와 같은 방법으로 TCP는 프로토콜 스택을 통해 알맞은 어플리케이션으로 이동하는 데이터를 라우트한다.

TCP는 문서적인 프로토콜이 아니다. **TCP는 연결 지향적이고 신뢰할 수 있는(reliable) 바이트스트림 서비스다.** 연결 지향은 TCP를 사용하는 두 어플리케이션은 데이터를 교환하기 전에 먼저 연결을 설정해야 함을 의미한다. 받는 패킷마다 전송을 확인하기 위한 확인 메시지가 발신자에게 보내지기 때문에 TCP는 신뢰할 수 있다. TCP는 받은 데이터를 에러 체크하기 위한 체크섬 또한 TCP의 헤더에 추가한다. TCP 헤더는 다음처럼 생겼다.

![Diagram 7 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e1d5ee51-84f2-42df-a47d-efbe1a94b217/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220131T144908Z&X-Amz-Expires=86400&X-Amz-Signature=a0cff8c2b36fae31f8c6408ea0c5a340ca66bcd74715e6808c819f6e70ffc0a7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 7 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

TCP 헤더에는 IP 주소를 위한 공간은 없다. TCP는 IP 주소에 대한 어떤 것도 알지 못한다. TCP의 역할은 어플리케이션 레벨 데이터를 안정적으로(reliably) 어플리케이션에서 어플리케이션으로 보내는 것이다. 컴퓨터에서 컴퓨터로 데이터를 보내는 것은 IP의 역할이다.

> 일반적으로 사용되는 인터넷 서비스의 포트 넘버들
FTP - 20/21
Telnet - 23
SMTP - 25
HTTP - 80
Quake III Arena - 27960
> 

## Internet Protocol

TCP와 달리 **IP는 신뢰할 수 없는 비연결형 프로토콜**이다. IP는 패킷이 목적지에 도착하는지에 대한 여부를 신경 쓰지 않는다. IP는 연결과 포트 넘버에 대해서도 모른다. **IP의 역할은 패킷을 다른 컴퓨터로 보내고 라우트하는 것이다.** IP 패킷은 독립적인 엔터티이며 순서가 맞지 않거나 아예 도착하지 않을 수도 있다. 패킷이 도착하고 올바른 순서로 있는지 확인하는 것은 TCP의 역할이다. IP가 TCP와 유일하게 같은 점은 데이터를 받고 IP 헤더 정보를 TCP 데이터에 추가하는 방식이다. IP 헤더는 다음처럼 생겼다.

![Diagram 8 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0114d99b-4bcf-4e96-a344-1114d9ff0d82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220131T143449Z&X-Amz-Expires=86400&X-Amz-Signature=be3e099a30f30827e125add9ec9f90aefcdac192aa9ac6116cc46605d5467ec2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 8 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

위 그림에서 IP 헤더에서 송신, 수신 컴퓨터의 IP 주소를 확인할 수 있다. 아래는 어플리케이션 계층을 지나, TCP 계층을 지나, IP 계층을 지난 후의 패킷의 모습이다. 어플리케이션 계층 데이터는 TCP 계층에서 나뉘고, TCP 헤더가 추가된다. 패킷은 IP 계층으로 이동한 뒤 IP 헤더가 추가된다. 그 후 패킷은 인터넷을 통해 전송된다.

![Diagram 8 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f7e5f991-cb73-481f-9c25-92ffca4592cb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220131%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220131T144129Z&X-Amz-Expires=86400&X-Amz-Signature=31512717f346582d8db2ba7da547340f4334561cd860e3282c7ef24bc05b7e79&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

Diagram 8 of [http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm](http://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

## Wrap Up

인터넷이 어떻게 작동하는지 알아보았다. 현재 IP 버전인 IPv4는 2^32개의 주소만 사용할 수 있다. 결국엔 모든 주소가 다 사용되고 말 것이다. IPv6가 연구 및 테스트 중에 있다.(2022년이지만 아직 IPv6는 표준으로 사용되고 있지는 않다.) 그 다음은 어떻게 될까? 인터넷은 미 국방부의 연구 프로젝트로서 시작된 후로 먼 길을 왔다. 인터넷이 어떻게 될지는 아무도 모른다. 하지만 한 가지는 확실하다. 인터넷은 다른 어떤 메커니즘도 이루어내지 못한 방식으로 세상을 통합할 것이다. 정보화 시대가 한창 진행 중이며 그 일부가 된 것을 기쁘게 생각한다.

Rus Shuler, 1998

Updates made 2002