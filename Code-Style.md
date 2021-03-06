# Introduction

Codestyle is incomplete now, so if you have some misunderstandings,
feel free to ask us any questions, and we’ll answer them and correct this document.

Also you might face some code parts which don’t correspond our codestyle.
In this case you can correct it and inform us.

## Embox codestyle

Mainly we use Kernighan and Ritchie (K&R) code style in the Embox project.
We don’t use national symbols in source code including comments.
Basic rules of code design are listed below.

### Text placement

The length of the rows should not exceed 80 characters.

The size of the function should be around of one screen.

### Tabs and Brackets

An example of a well-written functions:

```
int foo(void) {
    while (NULL != p) {
        for (i = 0; i < p->tabsize; i++) {
            if (p->tab[i] == x) {
                return i;
            }
        }
        return -1;
    }
}
```

```
int bar(void) {
    __asm__ __volatile__ (
        "lwi  %0, %1, 0;\n\t"
        "mfs     %0, rmsr;\n\t"
        "or   %0, r0, %2;\n\t"
        "mts   rmsr, %1, 0;\n\t" :
        "=r"(msr), "=&r"(tmp):
        "r"(status), "i"(MSR_VM_MASK) :
        "memory"
    );
}
```

**Comments to the example**:
 * We use tabs as the indentation, you should specify tab size in your editor as 4 spaces.
 * Shorthand notations are not allowed to use. Always put braces.
 * An opening brace is placed on the same line as the operand which it belongs to. Before a brace you should put one space.
 * A closing brace is placed on a new line at the same level as parent code.

### Blanks and blank lines

**Blanks**:
 * You should not place more than one blank lines in a row.
 * At the end of the file you should place one blank line.
 * You should place one blank line between the declarations or definitions of the functions and variables.
 * Local variable definitions are separated from code by one blank line.

We use standard style for the space character.

**One space is placed**:
 * between operators:
```
int a = x + y * (1 + b) / foo(11);
```
 * between constructs such as for/while/if/switch and brackets:
```
if (a < 7) {
  ...
}
```
 * in case of type casting:
```
int x = (int) ((double) a / 13 + 13);
```
**No space is placed**:
 * between a function definition and brackets:
```
int main(void) {
}
```
 * between a function call and brackets:
```
int x = foo(1);
```
 * before and after an increment/decrement operator:
```
i++;
```
 * between a pointer name and ```*```:
```
struct list_head *tmp;
```

### Macros

 * If a macro is multi-line you should place a backward slash at the end of each line in one space symbol.
 * Each macro argument must be put between brackets excepting string concatenation *##*. Macro parameters should differ from ordinary ones. For example:
```
#define MACRO(_field) struct somestruct ss = { .field = _field }
```
 * Any final statement-terminating semicolon should be supplied by the macro invocation rather than the macro. Pay attention on absence of semicolon
 after while (0).
```
#define MACRO(...) do { } while(0)
```

Examples of good macros:
```
#define INTERRUPT_NRS_TOTAL 16
```
```
#define interrupt_nr_valid(interrupt_nr) \
	((interrupt_nr_t) interrupt_nr < (interrupt_nr_t) INTERRUPT_NRS_TOTAL)
```
```
#define INTERRUPT_NR_CHECK(interrupt_nr)     \
  do {                                       \
    if (!interrupt_nr_valid(interrupt_nr)) { \
      printf("Invalid interrupt number");    \
      return -EINVAL;                        \
    }                                        \
  } while (0)
```

### Naming

#### General requirements
Each entity must have a significant name. It is common to use
```underline_style_name```. Almost everywhere we use lower case.
Upper case is used in macro names and constant
names defined by #define.
#### Module naming
A module is consist of related entities. Each of them must begin with
a module-specific prefix.
#### Local variables
It is allowed to use common abridgments such as cnt, err, ret etc. in names of local variables. Variable names should be short but significant.
We use i, j, k for numeric iteration and i_entityname for list iteration.
#### Global variables and constants
Are you sure that you are not able to manage without global variables? Then you should name it as ```<module name>_r_<variable name>``` in order to make it distinctive from other variables. Global constants should be named as
```<module name>_c_<constant name>```.
#### Functions
Name format for functions is ```<module name>_<function name>``` even if
the function isn't exported. Function name should be clear and represent its action.
You should not use abridgments if you cannot prove its necessity. Compare
```count_active_users()``` and ```cntusr()```.

Not exported functions should be static.
#### Structures
A structure name may include a little specific prefix. It is convenient especially if structure consists of fields which name is the same as name of the some other structure field. For example:
```
struct net_interface { .ni_name, .ni_num, .ni_xxx }
```
#### Constants and macros
Only #define’d constants and macros have ```UPPER_СASE``` name. You can write a macro name in lower_case if it is used as an ordinary function, in other words, if the macro has no side effects.

### Conventional comments
 * Comment is an ordinary complete sentence which should be written in proper English.
 * Comments should include description of non-obvious behavior of a function.  For example, if a function must be called locked.
```
/** Called by critical dispatching code with IRQs disabled. */
static void sched_preempt(void) {
    sched_lock();
    __schedule(1);
    sched_unlock();
}
```
 * Try avoid excess commenting like “++i; // increments i”.
 * Keep comments in a relevant state. A comment that contradicts a code if worse than absence of it.
 * A code should consist of only English text, no transliteration is allowed. It concerns also naming functions and variables.
 * Only C-style comments are allowed:
```
/* ... */
```
 * Comments like *//...* are not allowed
 * Unused code blocks should be disabled by using the conditional compilation preprocessor
```
#if 0
  ... unused_code ...
#endif
```
 * Multi-line comments should begin with a star. At the end of a sentence a dot is placed and sections are separated with a blank line.
```
/* This code is necessary.
 *
 * Attention! It uses architecture-dependent code for SPARC.
 */
... Some code
```
 * At the beginning of the files and functions [Doxygen](http://www.stack.nl/~dimitri/doxygen/manual.html) comments should be written. At the first place it is about headers that contain module API.

Each file should start with:
```
/**
 * @file
 * @brief Short brief: starts with capital letter, point on the end.
 * @details Complete description. Possible to be written not on one line
 * Each line must be less then 80 symbols length. Each phrase ends with point.
 * Different paragraphs should be separated with empty line.
 * <empty line after description>
 * @date <creation date: dd.mm.yy>
 * @author <Name Surname of the first author>
 * @author <Name Surname>
 *         - <Changes description>
 *         - Doxygen understands any visual enhancement commands in this
 *           section, e.g. you may use hyphens to create a list of items.
 */
```
An example of such comment:
```
/**
 * @file
 * @brief IO Boards driver.
 * @details This driver defines generic operations with registers
 * of IO board's address space: @link #io_board_reg_load() load @endlink
 * and @link #io_board_reg_store() store @endlink.
 *
 * <b>Driver details</b>:
 * <table>
 * <tr><td>Bus</td>         <td>@c APB</td></tr>
 * <tr><td>Vendor ID</td>   <td>@c 0x08 (Terkom)</td></tr>
 * <tr><td>Device ID</td>   <td>@c 0x0A</td></tr>
 * <tr><td>Base</td>        <td>@c 0x80000B00</td></tr>
 * <tr><td>IRQ</td>         <td>@c --</td></tr>
 * </table>
 *
 * @date 18.12.08
 * @author Anton Bondarev
 *         - Initial implementation
 * @author Eldar Abusalimov
 *         - Reviewing, refactoring and documenting
 */
```

 * Each macro, type definition, function prototype, enumeration, union, structure, and its fields, must be particularly described in comments

```
/**
 * Checks if the specified irq_nr represents valid IRQ number.
 * @note The same as HAL @link interrupt_nr_valid() @endlink macro.
 */
#define irq_nr_valid(irq_nr) interrupt_nr_valid(irq_nr)

/**
 * Type representing interrupt request number.
 * @note The same as HAL #interrupt_nr_t type.
 */
typedef interrupt_nr_t irq_nr_t;

/**
 * Interrupt Service Routine type.
 *
 * @param irq_nr the number of interrupt request being handled
 * @param data the device tag specified at @link irq_attach() @endlink time
 *
 * @return interrupt handling result
 * @retval IRQ_NONE if ISR didn't handled the interrupt
 * @retval IRQ_HANDLED if interrupt has been handled by this ISR
 */
typedef irq_return_t (*irq_handler_t)(irq_nr_t irq_nr, void *data);

/**
 * Attaches @link #irq_handler_t interrupt service routine @endlink to the
 * specified @link #irq_nr_t IRQ number @endlink.
 *
 * @param irq_nr the IRQ number to attach the @c handler to
 * @param handler the ISR itself
 * @param flags TODO not yet implemented -- Eldar
 * @param data the optional device tag which will be passed to the ISR.
 * @param dev_name the optional device name
 *
 * @return attach result
 * @retval 0 if all is OK
 * @retval -EINVAL if @c irq_nr is not @link #irq_nr_valid() valid @endlink or
 *                 if the @c handler is @c NULL
 * @retval -EBUSY if another ISR has already been attached to the specified IRQ
 *                number
 * @retval -ENOSYS if kernel is compiled without IRQ support
 */
extern int irq_attach(irq_nr_t irq_nr, irq_handler_t handler,
    irq_flags_t flags, void *data, const char *dev_name);
```

### Header files
The body of header file should be organized in the following way:
```
#ifndef <subsystem_prefix>_<file_name>_H_
#define <subsystem_prefix>_<file_name>_H_

#endif /* <subsystem_prefix>_<file_name>_H_ */
```
