These examples demonstrate the use of handlers , which are similar to tasks, but get executed when notified by using a 'notify' keyword
from the task definition.  Even if you have multiple tasks in a playbook which noftify the same handler, it (handler) gets executed only once
after all the tasks are executed

The default behaviour of handlers is to get triggered at the end of the playbook after completion of all the tasks, however, this can be 
changed by using meta: flush_handlers after the task.  All the handlers defined in the hanlders: section get triggered when a playbook encounters
meta: flush_handlers, if the defined handlers were notified by any of the previous tasks before reaching the meta: flush_handlers.

