-(void)testGroupAndSemaphore{
    dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
    dispatch_group_t group = dispatch_group_create();
    
    dispatch_semaphore_t sem1 = dispatch_semaphore_create(0);
    dispatch_semaphore_t sem2 = dispatch_semaphore_create(0);
    dispatch_semaphore_t sem3 = dispatch_semaphore_create(0);
    
    dispatch_group_async(group, queue, ^{
        [self methodWithABlock:^{
            NSLog(@"group1 async");
            
            dispatch_semaphore_signal(sem1);
            
        } time:0.4 queue:queue];
        
        long semaphore = dispatch_semaphore_wait(sem1, dispatch_time(DISPATCH_TIME_NOW, DISPATCH_TIME_FOREVER));
        NSLog(@"group1 after");
        
    });
    //
    dispatch_group_async(group, queue, ^{
        
        [self methodWithABlock:^{
            NSLog(@"group2 async");
            dispatch_semaphore_signal(sem2);
            
        } time:0.1 queue:queue];
        
        long semaphore = dispatch_semaphore_wait(sem2, dispatch_time(DISPATCH_TIME_NOW, DISPATCH_TIME_FOREVER));
        
        NSLog(@"group2 after");
        
        
    });
    
    
    
    dispatch_group_async(group, queue, ^{
        
        
        [self methodWithABlock:^{
            NSLog(@"group3 async");
            
            dispatch_semaphore_signal(sem3);
            
        } time:0.2 queue:queue];
        
        
        long semaphore = dispatch_semaphore_wait(sem3, dispatch_time(DISPATCH_TIME_NOW, DISPATCH_TIME_FOREVER));
        NSLog(@"group3 after");
        
    });
    

    dispatch_group_notify(group, dispatch_get_main_queue(), ^{
        
        NSLog(@"UI");

    });
}

-(void)methodWithABlock:(CLGCDBlock)block time:(NSTimeInterval)time queue:(dispatch_queue_t)queue{
    if (block) {
        dispatch_queue_t queue_t = queue!=NULL?queue:dispatch_get_main_queue();
        
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(time * NSEC_PER_SEC)), queue_t, ^{
            block();
        });
        
    }
}