# DSA_easy
题目链接
http://www.cryptopals.com/sets/6/challenges/43
http://www.cryptopals.com/sets/6/challenges/44

1991年8月美国国家标准局(NIST)公布了数字签名标准(Digital Signature Standard, DSS)。此标准采用的算法称为
数字签名算法(Digital Signature Algorithm, DSA)，它作为ElGamal和Schnorr签名算法的变种，其安全性基于离散
对数难题；并且采用了Schnorr系统中，g为非本原元的做法，以降低其签名文件的长度。
算法中应用了下述参数：
p：L bits长的素数。L是64的倍数，范围是512到1024；
q：p - 1的160bits的素因子；
g：g = h^((p-1)/q) mod p，h满足h < p - 1, h^((p-1)/q) mod p > 1；
x：x < q，x为私钥 ；
y：y = g^x mod p ，( p, q, g, y )为公钥；
H( x )：One-Way Hash函数。DSS（FIPS186-4）中选用SHA-1或者SHA-2( Secure Hash Algorithm系列中的2个较新版本，其中SHA-2有4个，SHA-224，SHA-256，SHA-384，SHA-512，最原始的SHA已经不再被使用)。
p, q, g可由一组用户共享，但在实际应用中，使用公共模数可能会带来一定的威胁。签名及验证协议如下：
1. 产生随机数k，k < q；
2. 计算 r = ( g^k mod p ) mod q
s = ( k^(-1) (H(m) + xr)) mod q
签名结果是( m, r, s )。
3. 验证时计算 w = s^(-1)mod q
u1 = ( H( m ) * w ) mod q
u2 = ( r * w ) mod q
v = (( g^u1 * y^u2 ) mod p ) mod q
若v = r，则认为签名有效。