<template>
	<div class="header">
		<div class="header-name">
			<span class="header-name__greeting">Hi, Jane Doe</span>
			<div class="toggle">
				<span class="toggle__line"></span>
				<span class="toggle__line"></span>
				<span class="toggle__line"></span>
			</div>
		</div>
		<div class="header-main"></div>
	</div>
</template>

<script>

export default {
  name: 'Header'
}
</script>

<style type="text/css">
	.header-name {
		align-items: center;
		background: rgb(0,155,214);
		background: linear-gradient(140deg, rgba(0,155,214,1) 0%, rgba(54,207,213,1) 100%);
		color: white;
		display: flex;
		font-weight: 700;
		justify-content: space-between;
		padding: .75rem;
	}

	.toggle:hover {
		cursor: pointer;
	}

	.toggle__line {
		background-color: white;
		border-radius: 5px;
		display: block;
		height: 2px;
		margin: 4px 0;
		width: 24px;
	}

</style>