<template>
  <nav class="sidebar">
	<ul class="sidebar__nav-list">
		<li class="sidebar__nav-item">
			<a class="sidebar__nav-link sidebar__nav-link--active" href="">
				<span class="sidebar__nav-icon"><i class="fas fa-th-large"></i></span>
				<span class="sidebar__text">Dashboard</span></a>
		</li>
		<li class="sidebar__nav-item">
			<a class="sidebar__nav-link" href="">
				<span class="sidebar__nav-icon"><i class="fas fa-envelope"></i></span>
				<span class="sidebar__text">Messages</span>
				<span class="sidebar__notification">2</span>
			</a>
		</li>
		<li class="sidebar__nav-item">
			<a class="sidebar__nav-link" href="">
				<span class="sidebar__nav-icon"><i class="fas fa-user-cog"></i></span>
				<span class="sidebar__text">Admin</span>
			</a>
		</li>
		<li class="sidebar__nav-item">
			<a class="sidebar__nav-link" href="">
				<span class="sidebar__nav-icon"><i class="fas fa-sign-out-alt"></i></span>
				<span class="sidebar__text">Logout</span>
			</a>
		</li>
	</ul>
  </nav>
</template>

<script>
export default {
  name: 'Sidebar'
}
</script>

<style type="text/css">
	.sidebar {
		background-color: #081727;
	}

	.sidebar__nav-list {
		list-style: none;
		padding: 0;
	}

	.sidebar__nav-icon {
		margin-right: .75rem;
	}

	.sidebar__nav-link {
		border-top: 1px solid transparent;
		border-bottom: 1px solid transparent;
		color: white;
		display: flex;
		justify-content: space-between;
		padding: .5rem 1rem;
		text-decoration: none;
	}

	.sidebar__nav-link:hover {
		background-color: #263955;
	}

	.sidebar__nav-link--active {
		background-color: #263955;
		border-color: #00adef;
	}


	.sidebar__text {
		flex-grow: 1;
	}

	.sidebar__notification {
		background-color: #ffe980; 
		border-radius: 50%;
		color: #081727;
		font-size: .75rem;
		padding: .1rem .5rem;
	}
	
</style>