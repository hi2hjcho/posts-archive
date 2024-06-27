---
tags:
---

==상위노트==
- [[n0065'' 신호 및 시스템 signals and systems, TEXT collection]]   
- [[n0065_T11'' estimation FFT exact frequency]]  


[R01] > [[n0065_T11_R01'' Cedron articles DSPrelated]]   
- exact frequency formula for a pure real tone in a DFT (2015 April 20) / Cedron Dawg [Link](https://www.dsprelated.com/showarticle/773.php)
- comparison of frequency estimation (interpolation 3 DFT bins) algorithms
- article에서 제시된 다양한 방법에 대해서 numeric 정리 및 성능을 확인하기 위하여 자체적으로 실험 수행하여 [[n0065_T11'' estimation FFT exact frequency#C04 Cedron articles experiments|논문 준비 중 인노트 링크 - C04]]
- Cedron 추천 홈페이지에 유용한 자료 많음 - [tsdconseil 링크](http://www.tsdconseil.fr/log/scriptscilab/festim/index-en.html)
#### [R02] > High-Precision Fourier Analysis of Sounds Using Signal Derivatives


#### [R03] > Improved Fundamental Frequency Estimation Using Parametric Cubic Convolution


#### [R04] > On the Window selection for THREE FFT-Based High-Accuracy Frequency Estimation Methods / Hee-Suk PANG, 2005
- 정확한 주파수 찾기를 위한 접근법 3가지에 대해서 설명: zero-padding / PDA (Phase difference approximation, 페이즈 정보를 이용한 주파수 추정), WMIDFT (Weighted multipoint interpolated DFT, interpolation을 이용한 방법)
- 각 알고리즘과 window function 의 조합에 따른 성능 비교 / 알고리즘 제안 없음

#### [R05] | Weighted multipoint Interpolated DFT to Improve Amplitude estimation of Multifrequency signal

#### [R06_1] | Fast, Accurate Frequency estimators, Jacobsen / IEEE SPM
첨부된 논문에서 제안한 주요 주파수 추정 방법을 요약하면 다음과 같습니다:
1. 식 (3) 방법: Equation (3) fits a quadratic curve
	- 3개의 복소수 DFT 값 (Xk-1, Xk, Xk+1)을 이용
	- 보정 계수 δ = -Re[(Xk+1 - Xk-1) / (2Xk - Xk-1 - Xk+1)]
	- 계산이 단순하고 비교적 정확함
	- 단점은 직사각 윈도우에만 적합
![[Pasted image 20240605112215.png]]  

1. 식 (4) 방법: Equation (4) finds the center of mass of magnitudes
	- 3개의 DFT 진폭 값 (|Xk-1|, |Xk|, |Xk+1|)을 이용
	- 보정 계수 δ = P(|Xk+1| - |Xk-1|) / (|Xk| + |Xk-1| + |Xk+1|)
	- P는 윈도우 함수에 따라 스케일링 상수 값이 다름
	- 비직사각 윈도우에도 적용 가능
2. 식 (5) 방법: Equation (5) finds the amplitude-weighted average of bin frequencies
	- 3개의 복소수 DFT 값 (Xk-1, Xk, Xk+1)을 이용
	- 보정 계수 δ = Re[Q(Xk-1 - Xk+1) / (2Xk + Xk-1 + Xk+1)]
	- Q는 윈도우 함수별 스케일링 상수
	- 복소수 연산이지만 진폭 계산은 필요 없음
	- 비직사각 윈도우에도 적용 가능

이 방법들은 모두 DFT 결과의 3개 빈 값만을 이용하여 주파수 피크의 정확한 위치를 예측하는 비교적 단순한 알고리즘입니다. 특히 식 (4), (5)는 윈도우 함수 영향을 고려하여 보다 일반적인 경우에 적용할 수 있습니다.

The idea is to fit a quadratic curve through the three complex DFT samples Xk-1, Xk, Xk+1 around the peak bin k. The peak location is then estimated as the maximum of this quadratic curve, which gives the fractional correction δ to add to the integer bin index k.


#### [R06_2] | Jacobsen compilation - A Brief Examination of Current and a Proposed Find Frequency Estimator using THREE DFT samples / Eric Jacobsen 2015
- 1990년대 부터의 정밀 주파수 추정 알고리즘의 발전에 대해서 간략하게 설명
- Jacobsen, Candan, and Cedron 알고리즘에 대한 설명이 이어짐 / 알고리즘 간 서사는 없음. 단편적 서술.
#### [R07] > A High-Accuracy, High Anti-Noise, Unbiased Frequency Estimator Based on Three CZT Coefficients for Deep Space Exploration Mission
- 우주 / Chirp-Z Transform, 3개 주파수 빈 이용, 

#### [R08] > a Method for Fine Resolution Frequency estimation from THREE DFT samples / Candan, 2011
- 기존 Jacobian 방식에서 편향을 제거 할 수 있는 추가 텀을 이용한 비선형 관계식을 이용하여 정밀 주파수를 추정하여 **[R06_1] Jacobian 방식을 일반화**
![[Pasted image 20240605114242.png]]  

#### [R09] > Analysis and Further improvement of Fine Resolution Frequency estimation method from THREE DFT samples / Candan, 2013
==키워드==  MSE 에 대한 심도있는 논의 
==이론노트==  

해당 논문은 [R08] 논문의 개선 논문: 주요 개선점은 다음과 같습니다.
- 추정기의 bias(편향)와 MSE(평균제곱오차)에 대한 분석 수행
	- 기존 방법은 bias가 존재함을 지적
	- Bias가 MSE에 미치는 영향을 SNR에 따라 분석 (식 (8))
- Bias 제거를 통한 추정 성능 향상
	- 기존 추정치에 bias 제거 연산을 추가로 적용 (식 (21)) δ̃ = δ̂ / Δ(δ̂), 여기서 δ̂는 기존 추정치, Δ(·)는 bias 함수
	- 이를 통해 높은 SNR에서의 성능을 개선함
- 세밀한 MSE 분석
	- 낮은 MSE를 보장하는 SNR 임계값(threshold)을 해석적으로 유도 (식 (20))
	- Monte Carlo 시뮬레이션을 통해 이론적 분석의 타당성 입증
즉, 핵심적인 개선사항은 기존 방법의 bias를 분석하고 이를 제거하는 식 (21)을 도입함으로써, 높은 SNR에서 추정 성능을 향상시킨 것입니다. 또한 MSE 분석을 정교화하여 이론적 성능 예측의 정확도를 높인 점도 주목할 만합니다.
![[Pasted image 20240605115010.png]]  

Figure 2에서는 5개의 서로 다른 알고리즘 또는 결과를 비교하고 있습니다:
1. Monte Carlo simulations (파란색 실선) - 몬테카를로 시뮬레이션을 통해 얻은 제안된 방법의 MSE 결과  
2. Theoretical RMSE (하늘색 점선) - 식 (11)에서 유도된 제안된 방법의 이론적인 제곱근 MSE 
3. Gross error contribution (파란색 점선) - 식 (19)에서 유도된 gross error에 의한 MSE 상한
4. SNR threshold (검은색 별표) - 식 (20)에서 계산된 SNR threshold 
5. ML estimator (빨간색 실선) - Maximum Likelihood 추정기의 MSE 
그리고 모든 결과는 Cramer-Rao lower bound (녹색 점선)와 비교되고 있습니다.

#### [R10] > Fine resolution frequency estimation from THREE DFT samples: Case of windowed data / Candan, 2015
- Candan 본인이 제안한 알고리즘을 window 함수와 함께 사용시 발생하는 성능 차이에 대해서 다양한 각도에서 분석


#### [R13] | A high resolution fundamental frequency determination based on phase changes of the Fourier transform


#### [R14] | 음향측정: FFT 파라미터 * 수업자료 활용


#### [R15] > Accurate frequency estimator of sinusoid based on interpolation of FFT and DTFT, Fan 2020
This paper proposes an accurate frequency estimator for a complex sinusoid in additive white noise. The proposed method is based on **interpolation of the Fast Fourier Transform (FFT) and Discrete-Time Fourier Transform (DTFT).** The key steps are:
1. Zero-padding is first performed before taking the FFT of the sinusoid sampled data.
2. The coarse frequency estimate is obtained by finding the discrete frequency index of the maximum FFT spectrum line.
3. The fine frequency estimate is obtained by employing the maximum FFT spectrum line and two DTFT sample values located on the left and right side of the maximum FFT spectrum line. These DTFT samples are closer to the true DTFT peak than the neighboring FFT spectrum lines used in other methods.
4. The correlation coefficients between the Fourier transforms of the noise at different spectral lines are derived, since the spectral lines used are closely spaced.
5. Using these correlation coefficients, the mean squared error (MSE) calculation formula for the frequency estimate is derived for the additive white noise case.
The analytical and simulation results show that the proposed estimator has lower MSE compared to competing FFT interpolation based estimators, and its signal-to-noise ratio threshold is lower than other algorithms like Candan, AM and Djukanovic algorithms, at the cost of slightly higher computational complexity.
종합하면, 본 논문은 기존 FFT 기반 방법들과 달리 FFT와 DTFT 보간을 결합하는 새로운 접근 방식을 제안하고, 이론적 성능 분석과 함께 성능 우위를 실험적으로 입증했다는 특징이 있습니다.

FFT와 DTFT의 보간을 결합하는 접근 방식은 Section II에서 설명되어 있습니다.
구체적으로 Section II의 두 번째 단락부터 FFT와 DTFT 보간을 결합하는 과정이 기술되어 있습니다:
Zero-padding된 신호의 2N-point FFT를 수행하여 최댓값을 갖는 FFT 스펙트럼 라인으로부터 대략적 주파수 추정 (coarse frequency estimation)
최댓값 FFT 라인(index m)과 그 좌우의 DTFT 샘플 값(f=(m±0.5)Δf에서의 DTFT 값)을 이용하여 정밀 주파수 추정 (fine frequency estimation)
식 (4)-(11)에 걸쳐 이러한 과정이 수식적으로 표현되어 있습니다. 특히 식 (10)이 DTFT 샘플 값 S0, S0.5, S-0.5를 이용하여 주파수 추정치의 소수 부분(δ)을 계산하는 핵심 수식입니다.

==참고노트== [[n0818_T03'' 신호 및 시스템 해석 - 생도 수업]]  


[R16]
[R17]
[R18] | A noniterative frequency estimator with rational combination of three spectrum lines
[R19] | High-precision frequency estimation of real sinusoids with reduced computational complexity using a model-based matched-spectrum approach
[R21] | Fan, Lei, et al. "Frequency estimator of sinusoid by interpolated DFT method based on maximum sidelobe decay windows." Signal Processing 186 (2021): 108125.
- 주파수 추정 방법의 분류로 시간 도메인에서의 방법과 주파수 도메인에서의 방법이 소개되고 있다. 시간 도메인에서 어떻게 주파수를 추정한다는 말인가? ML 방법이란 것이 구체적으로 무엇이란 말인가? #미해결주제 
[R22] | comparative study of high accuracy frequency estimation methods
- FFT, IFFT interpolated FFT, IWPA iterative weighted phase averager, ESPRIT
- 기계 소음 신호 분석을 통한 오류 확인의 효용성에 대해서 설명 - 짧은 시간의 데이터를 가지고도 정확한 주파수를 분석 할 수 있도록

#### [R23] | Vincent, François, et al. "An Improved Fast Estimation of Single Frequency." IEEE Signal Processing Letters (2023).
==서브노트== [[n0065_T11_R23'' Vincent_2023]]  
==키워드==  MLE, 
==이론노트== [[n0016'' ESTIMATION Statistical SIGNAL Processing, Kay text collection]]  
- 본 논문 [R23]에서는 신호 $x(n)$ 의 푸리에 변환의 최대값을 찾는 방법으로 해석하고 있으나 챗지피티의 문답에서는 로그 우도 함수(Log-ML function) 혹은 cost function 을 관측값의 pdf 을 최대화하는 기준으로 문제를 풀이함 
	- [R23] re-written ML criterion 에서는 $$ C(\omega) = \sum_{n=0}^{N-1} |x(n)|^2 + 2\text{Re} \left[ \sum_{k=1}^{N-1} (N - k)R_x(k)e^{-i k\omega} \right] $$
	- 챗지피티 Cost function 형태는 $J(f) = \sum_{t=1}^{N} (x(t) - A \sin(2\pi f t + \phi))^2 )$ 로 정리됨

R09 논문의 Fig. 2에서 **Maximum Likelihood (ML) 기법을 이용한 주파수 추정 결과**는 다음과 같은 이론에 근거합니다. ML 주파수 추정기는 periodogram의 최댓값을 찾는 것과 동일합니다 (Kay, 1993). 이는 논문의 Section II에서 다음과 같이 언급되어 있습니다.
"The maximum likelihood (ML) frequency estimator is known to be the periodogram, ([3] Kay, p. 539). Typically, the periodogram search is implemented by calculating a large point Fast Fourier Transform (FFT) and searching for the maxima in the magnitude spectrum."
**ML 추정기는 점근적으로 최적(asymptotically optimal)인 성질**을 가집니다. 즉, 신호 대 잡음비(SNR)가 증가함에 따라 ML 추정기의 분산은 Cramer-Rao Lower Bound (CRLB)에 점근적으로 수렴합니다. 이는 다음 문장에서 확인할 수 있습니다.
"For sufficiently high number of FFT points, the error variance of the periodogram estimate is expected to approach the Cramer–Rao (CR) bound, , ([3], eq. (15.72)), as SNR increases."
따라서 Fig. 2에서 ML 기법의 결과는 이론적으로 최적에 가까운 성능을 보여주며, 이는 CRLB와 비교하여 검증되었습니다. ML 기법은 제안된 방법의 성능 평가를 위한 중요한 비교 대상으로 사용되었습니다.

첨부된 논문에서 제안하는 가장 핵심적인 아이디어는 **Extended Invariance Principle (EXIP)를 이용하여 ML 주파수 추정 문제를 간단한 두 단계 최적화 문제로 변환하는 것**입니다. 

구체적으로, ML criterion인 식 (10)을 보면
C(ω) = ∑|x(n)|^2 + 2Re[∑(N-k)R̂x(k)exp(-jkωk)]
여기서 ω = [ω1 ... ωN-1]^T 로 확장하면, closed-form solution을 얻을 수 있습니다.

이는 식 (11)과 같이 pulse-pair estimations을 제공합니다. 
ω̂k = (1/k)⟨R̂x(k)⟩

그 다음 EXIP를 이용하여 위의 중간 추정치들로부터 식 (12)와 같이 원래의 ML 추정치를 구할 수 있습니다. 
ω̂=argmin[ω̂-ω1]^T Q[ω̂-ω1],  ω∈[-π,π] 

여기서 Q는 FIM (Fisher Information Matrix)으로 식 (14)와 같이 주어집니다.
E[Q]=diag[2(N-k)k^2 A^2]_k=1,...,(N-1)

이렇게 얻어진 추정치 ω̂E는 식 (14)와 같이 autocorrelation의 가중합으로 표현되며, ML 추정치와 asymptotically equivalent합니다. 더 나아가 식 (16)과 같이 autocorrelation lag K를 제한하여 계산량을 줄일 수 있습니다. 흥미롭게도 이는 기존의 유명한 Fitz 추정기와 매우 유사한 형태를 가지나 가중치에 (N-k) 항이 추가된 형태입니다.
즉, EXIP를 통해 ML 문제를 autocorrelation 기반의 closed-form 가중합 문제로 변환하는 것이 본 논문의 핵심 아이디어라 할 수 있습니다.


#### [R23_27] S. Kay, "A fast and accurate single frequency estimator," in IEEE Transactions on Acoustics, Speech, and Signal Processing, vol. 37, no. 12, pp. 1987-1990, Dec. 1989, doi: 10.1109/29.45547.

==참고노트== [[n0016'' ESTIMATION Statistical SIGNAL Processing, Kay text collection#LSE (T05)]]  

**수식 (7)의 유도 과정**은 다음과 같습니다
**1. 신호 모델**
먼저, 차분된 위상 데이터 Δt가 유색 가우시안 노이즈 프로세스의 평균 ω0를 추정하는 문제로 변환되었습니다.
$$ x_t = Ae^{j(ω_0\ t \ + \ θ)} + z_t, \ \ \ \  t = 0, 1, 2, ..., N - 1 $$
$$ x_t ≈ Ae^{j \ (ω_0 \ t \ + \ θ \ + \ u_t)} $$

**2. MLE = LSE** - 이러한 선형 모델에서 최대우도추정량(MLE)은 일반화된 최소제곱법(Generalized Least Squares)과 동일합니다.

**3. WLS cost function** - 일반화된 최소제곱법의 비용 함수 J는 다음과 같이 정의됩니다:
$$J = (\Delta - \omega_0 \mathbf{1})^T \ \mathbf{C}^{-1} \ (\Delta - \omega_0 \mathbf{1})$$
where $\Delta = [\Delta_0 , \ \Delta_1 , \ \cdots \ , \Delta_{N-2}]^T$, $\mathbf{1} = [1, \ 1, \ \cdots \ , 1]^T$, and $\mathbf{C}$  is the $(N-1) \times (N-1)$ covariance matrix of $\Delta$. 

4. 이 비용 함수를 ω0에 대해 최소화하면 MLE를 얻을 수 있습니다.
5. J를 ω0에 대해 미분하고 0으로 놓으면:
   ∂J/∂ω0 = -2 1^T C^(-1) (Δ - ω0 1) = 0
**6. MLE -> LSE 에 의한 파라미터 $\omega_0$ estimator**

$$\hat{\omega}_0 = \frac{\mathbf{1}^T \ \mathbf{C}^{-1} \ \Delta} {\mathbf{1}^T \ \mathbf{C}^{-1} \ \mathbf{1}} \tag{7}$$

$$\mathbf{1}^T \mathbf{C}^{-1} \Delta = \frac{N(N^2 - 1)A^2} {6\sigma_z^2} \sum_{t=0}^{N-2} \ \textcolor{green}{w_t} \ \Delta_t$$
$$\mathbf{1}^T \mathbf{C}^{-1} \mathbf{1} = \frac{N(N^2 - 1)A^2}{6\sigma_z^2}$$

$$\textcolor{green}{w_t} = \frac{\frac{3}{2}^N} {N^2 - 1} \left\{ 1 - \left[ \frac{t - \left(\frac{N}{2} - 1\right)}{\frac{N}{2}} \right]^2 \right\}.$$
$$\hat{\omega}_0 = \sum_{t=0}^{N-2} \ w_t \ \Delta_t$$
$$\Delta_t = \angle x_{t+1} - \angle x_t = \angle x_t^* \ x_{t+1} \tag{10}$$

수식 (10)이 가능한 이유는 복소수의 성질과 위상 차이의 정의에 기반함.

1. 복소수의 표현:
   각 시간 t에서의 신호 x_t는 복소수로 표현될 수 있습니다. 즉, x_t = |x_t|e^(jθ_t) 형태입니다.

2. 위상 차이의 정의:
   Δ_t는 연속된 두 시간 샘플 간의 위상 차이를 나타냅니다.
   Δ_t = θ_(t+1) - θ_t

**3. 복소수의 곱과 위상**
   $$x_t^* \ x_{t+1} = (|x_t|e^{-j\theta_t}) \cdot (|x_{t+1}|e^{j\theta_{t+1}}) = |x_t||x_{t+1}|e^{j(\theta_{t+1} - \theta_t)}$$
$$\angle(x_t^* \ x_{t+1}) = \theta_{t+1} - \theta_t$$

5. 결과:
따라서, Δ_t = θ_(t+1) - θ_t = ∠(x_t* x_(t+1))
이 과정을 통해 Δ_t = ∠x_(t+1) - ∠x_t = ∠(x_t* x_(t+1))이 성립함을 알 수 있습니다.

이 방법의 장점은 직접적인 위상 차이 계산 대신 복소수 곱의 각도를 사용함으로써, 위상 언래핑 **(phase unwrapping)** 문제를 피할 수 있다는 것입니다. 위상 언래핑은 특히 낮은 SNR에서 어려울 수 있으므로, 이 방법은 계산상 더 안정적이고 효율적입니다.

$$\hat{\omega}_0 = \sum_{t=0}^{N-2} \textcolor{green}{w_t} \ \angle \ x_t^* \ x_{t+1}$$

가중치를 1/N-1 로 하는 경우 샘플 평균이 되어 버리고 다음과 같이 표현가능.
$$\hat{\omega}_0 = \frac{1}{N-1} \ \sum_{t=0}^{N-2} \textcolor{green}{\angle} \ x_t^* \ x_{t+1} \tag{17}$$

Phase unwrapping(위상 언래핑)은 신호 처리에서 중요한 개념으로, 특히 위상 정보를 다룰 때 발생하는 문제를 해결하는 과정입니다. 이를 이해하기 위해서는 다음 사항들을 알아야 합니다:

1. 위상의 주기성:
   위상은 본질적으로 2π 주기를 가집니다. 즉, θ와 θ + 2πn (n은 정수)는 같은 위상을 나타냅니다.

2. 위상 측정의 한계:
   대부분의 시스템에서 위상은 -π에서 π 사이의 값으로 측정됩니다. 이를 "wrapped phase"라고 합니다.

3. 위상 점프 문제:
   연속적인 신호에서 실제 위상이 π를 넘어가면, 측정된 위상은 갑자기 -π로 "점프"합니다. 이는 실제 신호의 연속성을 해칩니다.

4. Phase unwrapping의 목적:
   이러한 인위적인 점프를 제거하고, 실제 연속적인 위상 변화를 복원하는 것입니다.

5. 과정:
   일반적으로 연속된 샘플 간의 위상 차이를 관찰하고, 큰 점프가 발생하면 2π의 배수를 더하거나 빼서 연속성을 유지합니다.

6. 어려움:
   노이즈가 있는 환경에서는 실제 위상 변화와 노이즈로 인한 변동을 구분하기 어려워 정확한 unwrapping이 어려울 수 있습니다.

앞서 논의된 방법(식 10)은 직접적인 위상 차이 대신 복소수 곱의 각도를 사용함으로써 이러한 unwrapping 과정을 피할 수 있게 해줍니다. 이는 특히 노이즈가 많은 환경에서 더 안정적인 결과를 제공할 수 있습니다.




#### [R24] > Jacobsen, Eric. "On local interpolation of DFT outputs." Online: http://www.ericjacobsen.org/FTinterp.pdf (1994).
![[Pasted image 20240605100733.png]]  

quadratic curve peak 을 찾는 방법을 통해서 fine frequency 찾기


#### [R25] Rife, "Single tone parameter estimation from discrete-time observations." IEEE Transactions on information theory 20.5 (1974): 591-598. 
이 논문은 "IEEE Transactions on Information Theory"에 1974년 9월에 발표된 David C. Rife와 Robert R. Boorstyn의 연구로, 잡음이 있는 이산 시간 관측치로부터 단일 주파수 톤의 매개변수를 추정하는 문제를 다루고 있습니다. 이 연구는 데이터 세트 테스트, 전화 전송 시스템 테스트, 레이더 및 기타 측정 상황에 응용될 수 있습니다.

논문은 주요 매개변수(주파수, 진폭, 위상)를 추정하는 방법을 제시하며, 이를 위해 Cramer-Rao 경계와 MLE (최대 우도 추정) 알고리즘을 도출했습니다. 특히, 최대 우도 추정(MLE) 방법의 성질을 증명하고, 이산 푸리에 변환(DFT)과의 관계를 활용하여 실용적인 알고리즘을 개발했습니다.

또한, 시뮬레이션 결과를 통해 이 알고리즘들의 성능을 검증했습니다. 특히 한 알고리즘의 임계 효과를 분석하여 다른 신호 대 잡음 비율(SNR)에서의 성능 변화를 비교했습니다. 샘플링 비율은 일정하며, 신호와 잡음은 대역 제한된 것으로 가정했습니다.

이 연구는 이론적 도출과 시뮬레이션 결과를 통해 MLE 추정기가 높은 SNR에서 CR 경계에 거의 도달함을 보여줍니다. 제안된 방법들은 통신, 레이더, 신호 처리 등 잡음 데이터로부터 정확한 매개변수 추정이 필요한 다양한 분야에 응용될 수 있습니다.

#### [R26] Lank, "A semi coherent detection and Doppler estimation statistic." IEEE Transactions on Aerospace and Electronic Systems 2 (1973): 151-165.


#### [R28] Pulse Pair Estimation of Doppler Spectrum Parameters

Pulse-pair technique은 레이더 신호 처리에서 주로 사용되는 방법으로, 특히 도플러 속도 추정에 널리 활용됩니다. 이 기법의 주요 특징과 원리는 다음과 같습니다:

1. 기본 원리:
   - 연속된 두 펄스(pulse pair) 사이의 위상 차이를 이용하여 목표물의 속도를 추정합니다.

2. 작동 방식:
   - 레이더가 연속된 두 펄스를 발사하고 반사된 신호를 수신합니다.
   - 두 반사 신호 사이의 위상 차이를 측정합니다.
   - 이 위상 차이는 목표물의 움직임에 의한 도플러 주파수 시프트와 관련이 있습니다.

3. 수학적 표현:
   - 속도 추정: v = (λ/4π) * (Δφ/ΔT)
     여기서, λ는 레이더 파장, Δφ는 위상 차이, ΔT는 펄스 간 시간 간격입니다.

4. 장점:
   - 계산이 간단하고 빠릅니다.
   - 하드웨어 구현이 비교적 쉽습니다.
   - 실시간 처리에 적합합니다.

5. 한계:
   - 노이즈에 민감할 수 있습니다.
   - 위상 언래핑(phase unwrapping) 문제가 발생할 수 있습니다.
   - 단일 목표물이나 비슷한 속도의 다중 목표물에 대해 더 효과적입니다.

6. 응용 분야:
   - 기상 레이더에서 바람의 속도 측정
   - 군사용 레이더에서 이동 목표물 추적
   - 교통 모니터링 시스템

Pulse-pair technique은 그 단순성과 효율성 때문에 많은 레이더 시스템에서 여전히 널리 사용되고 있습니다. 그러나 더 복잡한 환경이나 높은 정확도가 요구되는 상황에서는 더 정교한 알고리즘과 함께 사용되거나 대체되기도 합니다.


