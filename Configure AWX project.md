# Configure AWX project

Go to the projects menu and click "Add"

![e097bc9a23baea57f6d5beb968720741.png](../_resources/e097bc9a23baea57f6d5beb968720741.png)

Enter a name for the project, select "Git" as "Source Controle Type"

Enter: https://github.com/antuelle78/awx-install-on-k3s.git as "Source Controle URL" and click "Save".

![4e92c2101b3d9ad52b4f87a43b1d9949.png](../_resources/4e92c2101b3d9ad52b4f87a43b1d9949.png)

AWX will immediately start the initial sync task.

![b3cbd4c0faa2a7637b6c875d0ffcc2e4.png](../_resources/b3cbd4c0faa2a7637b6c875d0ffcc2e4.png)

You can click the job status to follow output.

![3d2fc064544caccf8091ebec2fd380cc.png](../_resources/3d2fc064544caccf8091ebec2fd380cc.png)

## Add job template

Go to "Templates" and click "Add" and select "Add job template"

![fcae966019f0bdbd9359f3b76b0ae50f.png](../_resources/fcae966019f0bdbd9359f3b76b0ae50f.png)

Enter a name, select the project added in previous step, the "deploy.yml" playbook should automatically selected.
See documentation for additional configuration options.

![2e4f32c9207bda8ad878cec501ce7afb.png](../_resources/2e4f32c9207bda8ad878cec501ce7afb.png)