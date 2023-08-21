# Viva Real Estate Laravel and Livewire Code Components Documentation

## Table of Contents

- [Viva Real Estate Laravel and Livewire Code Components Documentation](#viva-real-estate-laravel-and-livewire-code-components-documentation)
  - [Table of Contents](#table-of-contents)
  - [Laravel Controller: Dashboard](#laravel-controller-dashboard)
  - [Blade View: Dashboard](#blade-view-dashboard)
    - [Overview](#overview)
    - [Sidebar Navigation](#sidebar-navigation)
    - [Content Sections](#content-sections)
      - [Welcome Msg Content](#welcome-msg-content)
      - [Profile Content](#profile-content)
      - [Blog Content](#blog-content)
      - [Listings Content](#listings-content)
        - [Tabs](#tabs)
          - [Property Overview Tab](#property-overview-tab)
          - [Property Pending Tab](#property-pending-tab)
          - [Property Active Tab](#property-active-tab)
          - [Property Active Tab](#property-active-tab-1)
          - [Property Closed Tab](#property-closed-tab)
          - [Property Add New Tab](#property-add-new-tab)
          - [Property Add Picture's Tab](#property-add-pictures-tab)
        - [Content](#content)
          - [Property Overview Pane](#property-overview-pane)
          - [Property Pending Pane](#property-pending-pane)
          - [Property Active Pane](#property-active-pane)
          - [Property Closed Pane](#property-closed-pane)
          - [Property Add New Pane](#property-add-new-pane)
          - [Property Add Picture's Pane](#property-add-pictures-pane)
      - [User Content](#user-content)
        - [Tabs](#tabs-1)
          - [User Overview Tab](#user-overview-tab)
          - [User Manage Agents Tab](#user-manage-agents-tab)
        - [Content](#content-1)
          - [User Overview Pane](#user-overview-pane)
          - [User Manage Agents Pane](#user-manage-agents-pane)
      - [Settings Content](#settings-content)

## Laravel Controller: Dashboard

<--- [Laravel Controller: Dashboard](index.md).

## Blade View: Dashboard

The Blade view for the dashboard plays a vital role in presenting the user interface and providing access to various dashboard functionalities in the Viva Real Estate project. This view integrates Livewire components to dynamically render different content based on user interactions.

### Overview

The dashboard view is a central hub for users to manage their profile, interact with the messenger, access blog content, manage property listings, handle user management, and configure settings. Each section of the dashboard is dynamically rendered through Livewire components, ensuring a seamless and interactive user experience.

```blade
@extends('dashboard.layout.head')

@section('sidebar')
{!! $htmlElements->Sidebar_Button('person-lines-fill', 'profile', 'Profile', 'selectTab("profile")') !!}
{!! $htmlElements->Sidebar_Button('chat-text', 'messenger', 'Messenger', 'selectTab("messenger")') !!}
{!! $htmlElements->Sidebar_Button('postcard', 'blog', 'Blog', 'selectTab("blog")') !!}

@if ($role === 'Admin')
{!! $htmlElements->Sidebar_Button('card-checklist', 'listings', 'Listings', 'selectTab("listings")') !!}
{!! $htmlElements->Sidebar_Button('people', 'users', 'Users', 'selectTab("users")') !!}
@endif

{!! $htmlElements->Sidebar_Button('gear', 'settings', 'Settings', 'selectTab("settings")') !!}
@endsection

@section('content')
<div class="welcome-msg" id="welcome-msg">
    <p>Welcome to the dashboard.</p>
    <p>Please select a tab on the left.</p>
</div>

<div class="profile-content" id="profile-content" hidden=''>
    @livewire('dashboard.profile', ['user' => $user])
    @livewire('dashboard.profile-edit-account', ['user' => $user])
    @livewire('dashboard.profile-edit-personal', ['user' => $user])
    @livewire('dashboard.profile-edit-professional', ['user' => $user])
</div>

<div class="blog-content" id="blog-content" hidden=''>
    @include('blog.index')
</div>

<div class="messenger-content" id="messenger-content" hidden=''>
    //
</div>

<div class="listings-content m-1" id="listings-content" hidden=''>

    <ul class="nav nav-tabs" id="agent_settings_tabs" role="tablist">
        <li class="nav-item" role="presentation">
            <button class="nav-link active" id="property-overview-tab" data-bs-toggle="tab"
                data-bs-target="#property-overview" type="button" role="tab" aria-controls="property-overview"
                aria-selected="true">
                <small>Overview</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="property-pending-tab" data-bs-toggle="tab" data-bs-target="#property-pending"
                type="button" role="tab" aria-controls="property-pending" aria-selected="true">
                <small>Pending</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="property-active-tab" data-bs-toggle="tab" data-bs-target="#property-active"
                type="button" role="tab" aria-controls="property-active" aria-selected="true">
                <small>Active</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="property-closed-tab" data-bs-toggle="tab" data-bs-target="#property-closed"
                type="button" role="tab" aria-controls="property-closed" aria-selected="true">
                <small>Closed</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="property-new-tab" data-bs-toggle="tab" data-bs-target="#property-new"
                type="button" role="tab" aria-controls="property-new" aria-selected="true">
                <small>Add New</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="new-picture-tab" data-bs-toggle="tab" data-bs-target="#new-picture"
                type="button" role="tab" aria-controls="new-picture" aria-selected="true">
                <small>Add Picture's</small>
            </button>
        </li>

    </ul>

    <div class="tab-content p-1 border border-top-0">
        <div class="tab-pane active" id="property-overview" role="tabpanel" aria-labelledby="property-overview-tab"
            tabindex="0">
            @livewire('dashboard.properties-overview')
        </div>

        <div class="tab-pane" id="property-pending" role="tabpanel" aria-labelledby="property-pending-tab" tabindex="1">
            @livewire('dashboard.properties-pending')
        </div>

        <div class="tab-pane" id="property-active" role="tabpanel" aria-labelledby="property-active-tab" tabindex="2">
            @livewire('dashboard.properties-active')
        </div>

        <div class="tab-pane" id="property-closed" role="tabpanel" aria-labelledby="property-closed-tab" tabindex="3">
            @livewire('dashboard.properties-closed')
        </div>

        <div class="tab-pane" id="property-new" role="tabpanel" aria-labelledby="property-new-tab" tabindex="4">
            @livewire('dashboard.properties.new-property')
        </div>

        <div class="tab-pane" id="new-picture" role="tabpanel" aria-labelledby="new-picture-tab" tabindex="4">
            @livewire('dashboard.properties.new-picture')
        </div>

    </div>
</div>

<div class="users-content" id="users-content" hidden=''>
    <ul class="nav nav-tabs" id="agent_settings_tabs" role="tablist">
        <li class="nav-item" role="presentation">
            <button class="nav-link active" id="user_overview_tab" data-bs-toggle="tab" data-bs-target="#user_overview"
                type="button" role="tab" aria-controls="user_overview" aria-selected="true">
                <small>Overview</small>
            </button>
        </li>

        <li class="nav-item" role="presentation">
            <button class="nav-link" id="manage_agents_tab" data-bs-toggle="tab" data-bs-target="#manage_agents"
                type="button" role="tab" aria-controls="manage_agents" aria-selected="false">
                <small>Manage Agents</small>
            </button>
        </li>
    </ul>

    <div class="tab-content p-1 border border-top-0">
        <div class="tab-pane active" id="user_overview" role="tabpanel" aria-labelledby="user_overview_tab"
            tabindex="0">
            @livewire('dashboard.user-overview')
        </div>
        <div class="tab-pane" id="manage_agents" role="tabpanel" aria-labelledby="manage_agents_tab" tabindex="1">
            @livewire('dashboard.user-management', ['user' => $user])
        </div>
    </div>
</div>

<div class="settings-content" id="settings-content" hidden=''>
    Settings
</div>
@endsection
```

### Sidebar Navigation

The sidebar section contains navigation buttons that allow users to switch between different dashboard tabs and sections. The content of the sidebar varies based on the user's role.

```blade
@extends('dashboard.layout.head')

@section('sidebar')

{!! $htmlElements->Sidebar_Button('person-lines-fill', 'profile', 'Profile', 'selectTab("profile")') !!}
{!! $htmlElements->Sidebar_Button('chat-text', 'messenger', 'Messenger', 'selectTab("messenger")') !!}
{!! $htmlElements->Sidebar_Button('postcard', 'blog', 'Blog', 'selectTab("blog")') !!}

@if ($role === 'Admin')
{!! $htmlElements->Sidebar_Button('card-checklist', 'listings', 'Listings', 'selectTab("listings")') !!}
{!! $htmlElements->Sidebar_Button('people', 'users', 'Users', 'selectTab("users")') !!}
@endif

{!! $htmlElements->Sidebar_Button('gear', 'settings', 'Settings', 'selectTab("settings")') !!}

@endsection
```

### Content Sections

The dashboard view dynamically displays content based on the selected tab. Livewire components are integrated to handle specific functionalities in each section.

```blade
@section('content')

// ...

@endsection
```

#### Welcome Msg Content

```blade
<div class="welcome-msg" id="welcome-msg">
  <p>Welcome to the dashboard.</p>
  <p>Please select a tab on the left.</p>
</div>
```

#### Profile Content

```blade
<div class="profile-content" id="profile-content" hidden=''>
  @livewire('dashboard.profile', ['user' => $user])
  @livewire('dashboard.profile-edit-account', ['user' => $user])
  @livewire('dashboard.profile-edit-personal', ['user' => $user])
  @livewire('dashboard.profile-edit-professional', ['user' => $user])
</div>
```

#### Blog Content

```blade
<div class="blog-content" id="blog-content" hidden=''>
    @include('blog.index')
</div>
```

goto [Livewire: Dashboard-Listings-Pending](Blog/index.md)

#### Listings Content

The listings section showcases different tabs for property management.

```blade
<div class="listings-content m-1" id="listings-content" hidden=''>
  <!-- Tabs for property management -->
  <!-- Livewire components are used for each tab -->
</div>
```

##### Tabs

```blade
<ul class="nav nav-tabs" id="agent_settings_tabs" role="tablist">

    // ...

</ul>
```

###### Property Overview Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link active" id="property-overview-tab" data-bs-toggle="tab" data-bs-target="#property-overview"
    type="button" role="tab" aria-controls="property-overview" aria-selected="true">
    <small>Overview</small>
    </button>
</li>
```

###### Property Pending Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="property-pending-tab" data-bs-toggle="tab" data-bs-target="#property-pending"
    type="button" role="tab" aria-controls="property-pending" aria-selected="true">
    <small>Pending</small>
    </button>
</li>
```

###### Property Active Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="property-active-tab" data-bs-toggle="tab" data-bs-target="#property-active"
    type="button" role="tab" aria-controls="property-active" aria-selected="true">
    <small>Active</small>
    </button>
</li>
```

###### Property Active Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="property-active-tab" data-bs-toggle="tab" data-bs-target="#property-active"
    type="button" role="tab" aria-controls="property-active" aria-selected="true">
    <small>Active</small>
    </button>
</li>
```

###### Property Closed Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="property-closed-tab" data-bs-toggle="tab" data-bs-target="#property-closed"
    type="button" role="tab" aria-controls="property-closed" aria-selected="true">
    <small>Closed</small>
    </button>
</li>
```

###### Property Add New Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="property-new-tab" data-bs-toggle="tab" data-bs-target="#property-new"
    type="button" role="tab" aria-controls="property-new" aria-selected="true">
    <small>Add New</small>
    </button>
</li>
```

###### Property Add Picture's Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="new-picture-tab" data-bs-toggle="tab" data-bs-target="#new-picture"
    type="button" role="tab" aria-controls="new-picture" aria-selected="true">
    <small>Add Picture's</small>
    </button>
</li>
```

##### Content

```blade
<div class="tab-content p-1 border border-top-0">

    // ...

</div>
```

###### Property Overview Pane

```blade
<div class="tab-pane active" id="property-overview" role="tabpanel" aria-labelledby="property-overview-tab" tabindex="0">
    @livewire('dashboard.properties-overview')
</div>
```

goto [Livewire: Dashboard-Listings-Overview](Listings/overview.md)

###### Property Pending Pane

```blade
<div class="tab-pane" id="property-pending" role="tabpanel" aria-labelledby="property-pending-tab" tabindex="1">
    @livewire('dashboard.properties-pending')
</div>
```

goto [Livewire: Dashboard-Listings-Pending](Listings/pending.md)

###### Property Active Pane

```blade
<div class="tab-pane" id="property-active" role="tabpanel" aria-labelledby="property-active-tab" tabindex="2">
    @livewire('dashboard.properties-active')
</div>
```

goto [Livewire: Dashboard-Listings-Active](Listings/active.md)

###### Property Closed Pane

```blade
<div class="tab-pane" id="property-closed" role="tabpanel" aria-labelledby="property-closed-tab" tabindex="3">
    @livewire('dashboard.properties-closed')
</div>
```

goto [Livewire: Dashboard-Listings-Closed](Listings/closed.md)

###### Property Add New Pane

```blade
<div class="tab-pane" id="property-new" role="tabpanel" aria-labelledby="property-new-tab" tabindex="4">
    @livewire('dashboard.properties.new-property')
</div>
```

goto [Livewire: Dashboard-Listings-Add New](Listings/new.md)

###### Property Add Picture's Pane

```blade
<div class="tab-pane" id="new-picture" role="tabpanel" aria-labelledby="new-picture-tab" tabindex="4">
    @livewire('dashboard.properties.new-picture')
</div>
```

goto [Livewire: Dashboard-Listings-Add Picture's](Listings/newpic.md)

#### User Content

The users section includes tabs for managing user-related information.

```blade
<div class="users-content" id="users-content" hidden=''>
  <!-- Tabs for user management -->
  <!-- Livewire components are used for each tab -->
</div>
```

##### Tabs

```blade
    <ul class="nav nav-tabs" id="agent_settings_tabs" role="tablist">

        // ...

    </ul>
```

###### User Overview Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link active" id="user_overview_tab" data-bs-toggle="tab" data-bs-target="#user_overview"
        type="button" role="tab" aria-controls="user_overview" aria-selected="true">
        <small>Overview</small>
    </button>
</li>
```

###### User Manage Agents Tab

```blade
<li class="nav-item" role="presentation">
    <button class="nav-link" id="manage_agents_tab" data-bs-toggle="tab" data-bs-target="#manage_agents"
        type="button" role="tab" aria-controls="manage_agents" aria-selected="false">
        <small>Manage Agents</small>
    </button>
</li>
```

##### Content

```blade
<div class="tab-content p-1 border border-top-0">

    /// ...

</div>
```

###### User Overview Pane

```blade
<div class="tab-pane active" id="user_overview" role="tabpanel" aria-labelledby="user_overview_tab" tabindex="0">
    @livewire('dashboard.user-overview')
</div>
```

goto [Livewire: Dashboard-User-Overview](User/overview.md)

###### User Manage Agents Pane

```blade
<div class="tab-pane" id="manage_agents" role="tabpanel" aria-labelledby="manage_agents_tab" tabindex="1">
    @livewire('dashboard.user-management', ['user' => $user])
</div>
```

goto [Livewire: Dashboard-User-Manage Agent's](User/manage_agent.md)

#### Settings Content

The settings section displays general settings information.

```blade
<div class="settings-content" id="settings-content" hidden=''>
  Settings
</div>
```
