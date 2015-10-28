<?php
	

	$dbc=mysqli_connect('localhost','root','','facemash') or die(mysqli_error());
	$using="use facemash";
	$query=mysqli_query($dbc, "select *from facemashed") or die ("Here it broke");
		if($_REQUEST!=NULL){
		$winner=$_REQUEST['won'];
		$loser=$_REQUEST['lost'];
		$base_rating=1400;
		$query2=mysqli_fetch_array(mysqli_query($dbc, "select rating from facemashed where id=$winner"));
		$query3=mysqli_fetch_array(mysqli_query($dbc, "select rating from facemashed where id=$loser"));
		$winner_rating=$query2['rating'];
		$loser_rating=$query3['rating'];

		if($winner_rating<=2100){ $Kw=32;} elseif($winner_rating>2100&&$winner_rating<2400){ $Kw=24;}elseif($winner_rating>2400){$Kw=16;}
		if($loser_rating<=2100){ $Kl=32;} elseif($loser_rating>2100&&$loser_rating<2400){ $Kl=24;}elseif($loser_rating>2400){$Kl=16;}

		$diff_w=($loser_rating-$winner_rating)/400;
		$diff_l=($winner_rating-$loser_rating)/400;
		
		$prob_winner=1/(1+pow(10,$diff_w));
		$prob_loser=1/(1+pow(10,$diff_w));

			$winner_rating = $winner_rating + $Kw*(1-$prob_winner);
			$loser_rating = $loser_rating + $Kw*(0-$prob_loser);

		$updatequery=mysqli_query($dbc,"update facemashed set rating=$winner_rating where id=$winner") or die(mysqli_error($dbc));
		$updatequery=mysqli_query($dbc,"update facemashed set rating=$loser_rating where id=$loser") or die(mysqli_error($dbc));
	}

		$max_ppl=80;

		$random1= rand(1,$max_ppl);
		$random2=rand(1,$max_ppl);
		while($random1===$random2)
		{ 
			$random1=rand(1,$max_ppl);
			$random2=rand(1,$max_ppl);
		}

		$rating1=mysqli_fetch_array(mysqli_query($dbc,"select rating from facemashed where id=$random1"));
		$rating2=mysqli_fetch_array(mysqli_query($dbc,"select rating from facemashed where id=$random2"));
		$ratingA=$rating1['rating'];
		$ratingB=$rating2['rating'];

?>
<!DOCTYPE html>
<html>
<head><title>Facemash</title>
<script type='text/javascript'>window.onbeforeunload=function(){}</script>
<link rel="stylesheet" href="main.css"/>
</head>
<body>
<div class="container">
	<div class="header"><h1>FACEMASH</h1></div>

	<div class="description">
	<h4> We let you judge and rate people, be it on their looks or personality. The criteria, it's in your hands!</h4>
	<h3>Who's better?</h3>
	</div>
	<div class="pics-container">
	<table class="pics">
	<tr>
	<td><a href='main.php?<?php echo "won=$random1&lost=$random2"; ?>'><img src="facepics/Image(<?php echo $random1; ?>).jpg" class="images"/></a></td>
	<td>OR</td>
	<td><a href='main.php?<?php echo "won=$random1&lost=$random2"; ?>'><img src="facepics/image(<?php echo $random2; ?>).jpg" class="images"/></a></td>
	<tr>
	<td>Rating:<?php echo $ratingA; ?></td><td></td><td>Rating: <?php echo $ratingB; ?></td>
	</table>
	</div>

	<div class="footer"> <table class="footer-links"><td>About</td>.<td>Rating</td></table></div>
</div>
</body>

</html>
