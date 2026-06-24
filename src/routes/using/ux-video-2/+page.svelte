<script>
    import { resolve } from '$app/paths';
</script>
<div class="subpage">
	<p>Watch a user experience video from Liverpool's Sarah Thompson:</p>
	<div class="eprase-video">
		<div class="iframe-aspect-wrapper">
			<video controls>
				<source src={resolve("/video/liverpool_user.mp4")} type="video/mp4">
				Your browser does not support the video tag.
			</video>
		</div>
	</div>
</div>