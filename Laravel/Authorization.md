1. Inline Authorization

```php
// app/HTTP/Controllers/JobController.php

public function edit(Job $job)  
{  
  
    if (Auth::guest()) {  
        return redirect('/login');  
    }  
  
    if ($job->employer->user->isNot(Auth::user())) {  
        abort(403);  
    }  
  
    return view('jobs.edit', ['job' => $job]);  
}
```

2. Gates

```php
// app/providers/AppServiceProvider.php

public function boot(): void  
{  
    Gate::define('edit-job', function (User $user, Job $job) {  
        return $job->employer->user->is($user);  
    });  
}

```

```php
// app/HTTP/Controllers/JobController.php

public function edit(Job $job)  
{  
      
    Gate::authorize('edit-job', $job);  
  
    return view('jobs.edit', ['job' => $job]);  
}
```


3. Can

In the controller:

```php

if (Auth::user()->cannot('edit-job', $job)) {  
     abort(403);  
}
```

is the equivalent of:

```php
Gate::authorize('edit-job', $job);  
```

```php
// app/HTTP/Controllers/JobController.php

public function edit(Job $job)  
{  
    if (Auth::user()->cannot('edit-job', $job)) {  
        abort(403);  
    }  
  
    return view('jobs.edit', ['job' => $job]);  
}
```

Can may be used in blade components. Below we only show a button if the user passed the gate i.e. can edit the job.

```php
@can('edit-job', $job)  
	<p class="mt-6">  
	    <a href="/jobs/{{ $job->id }}/edit">Edit Job</a>  
	</p>
@endcan
```

4. Middleware Authorization

```php
// routes/web.php

Route::get('/jobs', [JobController::class, 'index']);  
Route::get('/jobs/create', [JobController::class, 'create']);  
Route::get('/jobs/{job}', [JobController::class, 'show']);  
  
Route::post('/jobs', [JobController::class, 'store'])  
    ->middleware('auth');  
  
Route::get('/jobs/{job}/edit', [JobController::class, 'edit'])  
    ->middleware('auth')  
    ->can('edit-job', 'job');  
  
Route::patch('/jobs/{job}', [JobController::class, 'update']);  
Route::delete('/jobs/{job}', [JobController::class, 'destroy']);
```

5. Policies
```php
// app/Policies/JobPolicy.php

class JobPolicy  
{  
    public function edit(User $user, Job $job): bool  
    {  
        return $job->employer->user->is($user);  
    }  
}
```