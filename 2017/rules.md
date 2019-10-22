---
layout: base
title: Competition Rules
edition: "2017"
---

  <div class="row">
    <div class="col-xs-12">
      <p>The competition is run by the ORGANIZING COMMITTEE.</p>
    </div>
  </div>

  <div class="row with-counter">

    <div class="col-xs-12 col-lg-6">
      <h2>User accounts</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>Anyone can create an account and post one or several challenges and/or break one or more challenges on the WhibOx competition website.</p>
	  <p>The account owner may remain completely anonymous when creating an account. In addition to creating a login/password, an email address must be entered (in case the ORGANIZING COMMITTEE needs to contact the owner directly). However, the email address is not verified except for basic syntax. Users may e.g. enter their primary email address or, if they are willing to remain anonymous, may use a free service such as <a href="https://www.mailinator.com">Mailinator</a> to create an untraceable email address.</p>
	  <p>Therefore, the same person may create several accounts. User accounts are password-protected but passwords CANNOT BE CHANGED and are NOT RECOVERABLE in case of loss. It is the users' responsibility to choose a strong enough password and to keep it in a safe place. Non-anonymous winners will be asked to log in publicly during the prize ceremony.</p>
	  <p>Every newly registered user, referred to as a participant, is assigned a BANANA score initialized to 0.</p>
	  <p>The website is public in the sense that anyone can freely browse it (including downloading challenges) but logging in is required to post or break challenges.</p>
	  <p>The competition website is referred to as the SYSTEM.</p>
	</div>
      </div>
    </div>

    <div class="col-xs-12 col-lg-6">
      <h2>What is a challenge?</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>A challenge is a C source program that contains a function with prototype</p>
	  <pre>void AES_128_encrypt(unsigned char ciphertext[16], unsigned char plaintext[16]);</pre>
	  <p>The program must fulfill the following requirements:</p>
	  <ul>
	    <li>It implements an AES-128 encryption under some 128-bit key embedded into the code.</li>
	    <li>The function <code>AES_128_encrypt(ciphertext, plaintext)</code> takes a 128-bit plaintext block as input (as a pointer on an array of 16 bytes) and writes the corresponding 128-bit ciphertext (as an array of 16 bytes) at the given address.</li>
	    <li><strong>Requirements on the source:</strong></li>
	    <ul>
	      <li>The C language is the one accepted by GCC 6.2.3 with NO language dialect options. This is equivalent to the option <code>-std=gnu90</code>, meaning it is C90 with GNU extensions.</li>
	      <li>No <code>#include</code> or <code>extern</code> is allowed in the source code, and more generally linking to external libraries (even the standard C libraries) is forbidden. This is intended to prevent the inclusion of malware in submitted challenges. Any attempt to maliciously attack the SYSTEM or the computer system of attackers will lead to DISQUALIFICATION. In case evidence of malicious code is found in a challenge, contestants are invited to contact the ORGANIZING COMMITTEE directly (whibox.organizing.committee@gmail.com). If contestants are suspicious that some challenge program may contain malware, they may run GCC in docker or a virtual machine, exactly like the server does (using VirtualBox). Documentation on how the server runs is found on <a href="https://github.com/CryptoExperts/wb_contest_submission_server">GitHub</a>. Contestants are invited to download and install their own instance of the server if they want to ensure that their challenge will be accepted when submitted.</li>
	      <li>The type <code>unsigned long</code> is imposed to represent 32-bit integers, meaning that the target architecture is 32 bit oriented (as opposed to 64).</li>
	      <li>The source code must be completely portable and re-compilable towards ANY 32-bit target architecture. In other words, it must be made only of generic C which in particular, excludes the use of inline assembly.</li>
	      <li>The source code must be no bigger than <strong>50MB</strong>.</li>
	      <li>The REFERENCE COMPILER must use at most <strong>500MB</strong> of RAM to complete compilation.</li>
	      <li>The compilation must not exceed <strong>100 seconds</strong>.</li>
	    </ul>
	    <li><strong>Requirements on the executable:</strong> once compiled by the REFERENCE COMPILER, the executable program must:</li>
	    <ul>
	      <li>be <strong>20MB</strong> in size or less,</li>
	      <li>use <strong>20MB</strong> of RAM or less (this includes the stack and all global variables, at the exclusion of the code itself),</li>
	      <li>run, on average, in <strong>1 second</strong> or less per function call. This is not absolute time but CPU time, measured within a VirtualBox VM by the SYSTEM. Contestants may check that their challenges comply with this limitation by using the utility <code>ulimit</code> with the <code>-t</code> option.</li>
	    </ul>
	  </ul>
	  <p>The SYSTEM will reject a program that does not comply with these requirements.</p>
	  <p>Compliance with the requirements can be tested by downloading and running a local instance of the submission server found <a href="https://github.com/CryptoExperts/wb_contest_submission_server">here</a>.</p>
	  <p><strong>IPR and copyright disclaimer:</strong> contestants may indicate (typically in a header in their source) which license applies to their challenge program, if any.</p>
	</div>
      </div>
    </div>

    <div class="clearfix visible-lg-block"></div>

    <div class="col-xs-12 col-lg-7">
      <h2>Posting a challenge</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>A participant who posts a new challenge must temporarily reveal the embedded key to the SYSTEM for the purpose of verifying the consistency of the challenge program. The key is erased from the SYSTEM as soon as it has determined whether it is consistent or not with the challenge. This is done as follows.</p>
	  <p><strong>Challenge-key verification procedure:</strong></p>
	  <ol>
	    <li>The SYSTEM uses the REFERENCE IMPLEMENTATION of AES-128 to generate a number of random plaintext-ciphertext pairs under the given key. The number of pairs is determined by the SYSTEM but is at least 1000. Once this is done, the key is erased from the SYSTEM.</li>
	    <li>The SYSTEM compiles the challenge program and checks that it complies with the above requirements. If not, the challenge is rejected.</li>
	    <li>For each plaintext-ciphertext pair, the SYSTEM runs the executable on the plaintext and checks that the output is equal to the ciphertext.</li>
	    <li>In case of mismatch,</li>
	    <ol>
	      <li>the procedure halts,</li>
	      <li>the challenge program is rejected and</li>
	      <li>the mismatching plaintext-ciphertext pair is returned to the submitting participant.</li>
	    </ol>
	    <li>Otherwise, the challenge program is accepted and:</li>
	    <ol>
	      <li>given a name by the system,</li>
	      <li>declared as UNBROKEN,</li>
	      <li>assigned a STRAWBERRY score initialized to 0.</li>
	    </ol>
	  </ol>
	  <p>When accepted, the challenge is published on the website for anyone to download and play with. In addition, a small subset of random plaintext-ciphertext pairs is kept by the SYSTEM for later key verification. The number of pairs is determined by the SYSTEM but is at least 10.</p>
	</div>
      </div>
    </div>

    <div class="col-xs-12 col-lg-5">
      <h2>Winning strawberries</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>A participant may post challenges anytime between the STARTING DATE and the POSTING DEADLINE.</p>
	  <p>An UNBROKEN challenge gets more and more STRAWBERRIES as time goes by.</p>
	  <p>On the day the challenge is posted, its score is set to 0 STRAWBERRIES. After 24 hours, it gets 1 STRAWBERRY. After 48 hours, it gets 2 more STRAWBERRIES so that it has a total of 3 STRAWBERRIES. A challenge that is still UNBROKEN after \(n\) days receives \(n\) more STRAWBERRIES (so that its score increases quadratically with time).</p>
	  <p>When a challenge is BROKEN, the progression of its STRAWBERRY score is reversed. If the challenge has stayed UNBROKEN for \(n\) days, it looses 1 STRAWBERRY immediately, then \(n\) STRAWBERRIES 24 hours after it is declared BROKEN by the SYSTEM. It then looses another \(n-1\) STRAWBERRIES after 48 hours, and so forth, until its STRAWBERRY score reaches 0.</p>
	  <p>When the FINAL DEADLINE is reached, the STRAWBERRY scores of all challenges freeze.</p>
	</div>
      </div>
    </div>

    <div class="clearfix visible-lg-block"></div>

    <div class="col-xs-12 col-lg-7">
      <h2>Breaking challenges</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>A participant may break any challenge by submitting a putative key to the SYSTEM. The challenge may be UNBROKEN or already BROKEN.</p>
	  <p><strong>Key verification procedure:</strong> Given the submitted key, the SYSTEM fetches the recorded plaintext-ciphertext pairs attached to the challenge and uses the REFERENCE IMPLEMENTATION again to check that the key matches all the pairs. The key is erased as soon as the verification is completed.</p>
	  <p>In case of mismatch, the mismatching pair is returned to the submitting participant and the break is rejected.</p>
	  <p>Otherwise, the submitting participant is notified that the break is accepted. If the challenge was UNBROKEN, it is declared as BROKEN at the time the SYSTEM accepted the break.</p>
	  <p>Participants may break challenges until the FINAL DEADLINE.</p>
	</div>
      </div>
    </div>

    <div class="col-xs-12 col-lg-5">
      <h2>Winning bananas</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>A participant whose break has been accepted by the SYSTEM gets a chance to increase their BANANA score.</p>
	  <p>Noting \(S\) the current STRAWBERRY score of the challenge and \(B\) the participant's current BANANA score, \(B\) is updated as $$B = \max(B, S)\;.$$</p>
	</div>
      </div>
    </div>

    <div class="clearfix visible-lg-block"></div>

    <div class="col-xs-12 col-lg-7">
      <h2>Winning the competition</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>The winners are determined at the time of the FINAL DEADLINE. There are 2 winners, the STRAWBERRY WINNER and the BANANA WINNER.</p>
	  <h3>The strawberry winner</h3>
	  <p>The WINNING CHALLENGE is the challenge (BROKEN or UNBROKEN) which STRAWBERRY score has reached the highest peak between the STARTING DATE and the FINAL DEADLINE.</p>
	  <p>The STRAWBERRY WINNER is the participant who posted the WINNING CHALLENGE.</p>
	  <p>There may be several WINNING CHALLENGEs and STRAWBERRY WINNERs (no tie-breaking rule).</p>
	  <h3>The banana winner</h3>
	  <p>The BANANA WINNER is the participant with the highest BANANA score at the time of the FINAL DEADLINE.</p>
	  <p>There may be several BANANA WINNERs (no tie-breaking rule).</p>
	</div>
      </div>
    </div>

    <div class="col-xs-12 col-lg-5">
      <h2>Disqualification</h2>
      <div class="panel panel-default">
	<div class="panel-body">
	  <p>At any time, the ORGANIZING COMMITTEE may DISQUALIFY a participant in case of misconduct during the competition. Examples of misconduct include</p>
	  <ul>
	    <li>posting a challenge program that does not implement AES-128,</li>
	    <li>posting a challenge program that contains malware,</li>
	    <li>attempting to attack/hack the SYSTEM or the computer system of attackers in any manner.</li>
	  </ul>
	  <p>The user account of a DISQUALIFIED participant is disabled and challenges that the participant has posted may be withdrawn from the competition on a case-by-case basis.</p>
	</div>
      </div>
    </div>

    <div class="clearfix visible-lg-block"></div>

    <div class="col-xs-12">
      <h2>Terms of reference</h2>
      <h3>Important dates</h3>
      <div class="table-responsive">
	<table class="table table-striped table-bordered">
	  <tbody>
	    <tr><td>STARTING DATE</td><td>May 15, 2017 @ 00:00 UTC</td></tr>
	    <tr><td>POSTING DEADLINE</td><td>August 31, 2017 @ 23:59 UTC</td></tr>
	    <tr><td>FINAL DEADLINE</td><td>September 24, 2017 @ 12:00 UTC (1 day before CHES 2017)</td></tr>
	  </tbody>
	</table>
      </div>
      <h3>System and challenges</h3>
      <div class="table-responsive">
	<table class="table table-striped table-bordered">
	  <tbody>
	    <tr><td>SYSTEM</td><td>Server comprising the competition website and tools for compiling and testing challenge programs</td></tr>
	    <tr><td>REFERENCE COMPILER</td><td><code>gcc</code> with option <code>-nostdinc</code> (this is version 6.2.3 of <code>gcc</code>)</td></tr>
	    <tr><td>REFERENCE IMPLEMENTATION</td><td><code>aes.c</code> file available from <a href="https://github.com/CryptoExperts/wb_contest_submission_server">this GitHub repository</a>.</td></tr>
	    <tr><td>BROKEN (challenge)</td><td> At least one participant has been able to provide the SYSTEM with an AES-128 key that passes the key verification procedure.</td></tr>
	    <tr><td>UNBROKEN (challenge)</td><td>A challenge that is not BROKEN.</td></tr>
	  </tbody>
	</table>
      </div>
      <h3>Winning participants</h3>
      <div class="table-responsive">
	<table class="table table-striped table-bordered">
	  <tbody>
	    <tr><td>WINNING CHALLENGE</td><td>Challenge which STRAWBERRY score has reached the highest peak between the STARTING DATE and the FINAL DEADLINE.</td></tr>
	    <tr><td>STRAWBERRY WINNER</td><td>Participant who posted the WINNING CHALLENGE.</td></tr>
	    <tr><td>BANANA WINNER</td><td>Participant with the highest BANANA score at the time of the FINAL DEADLINE.</td></tr>
	    <tr><td>STRAWBERRY</td><td>🍓</td></tr>
	    <tr><td>BANANA</td><td>🍌</td></tr>
	    <tr><td>DISQUALIFIED (participant)</td><td> Misconducting participant excluded from the competition and whose challenges may be withdrawn.</td></tr>
	  </tbody>
	</table>
      </div>
    </div>
  </div><!-- .row -->


  <script type="text/javascript" async
	  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
  </script>
